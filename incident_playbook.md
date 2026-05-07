# incident_playbook.md

# DebateAI Incident Playbook — AI dẫn chứng sai và bắt đầu viral

**Startup:** DebateAI  
**Tình huống:** 9h30 sáng, một customer tweet screenshot cho thấy AI của DebateAI đưa dẫn chứng / luận điểm sai nghiêm trọng, có thể liên quan đến luật hoặc xuyên tạc lịch sử. Tweet đạt 200 retweets trong 30 phút và đang có signal viral.  
**Owner:** Founder  
**Backup owner:** Tech Lead  
**Mục tiêu:** Contain incident trong **30 phút đầu**.

---

## 0. 30-Second Founder Checklist

| Mốc thời gian | Quyết định | Hành động cụ thể |
|---|---|---|
| 0–5 phút | Verify | Mở Helicone, lọc 9:00–9:40, tìm `session_id`, text trong screenshot, email/user nếu có |
| Phút thứ 5 | Nếu chưa chắc | Giả định screenshot có thể là thật. Không chờ đủ bằng chứng mới hành động |
| 5–15 phút | Stop bleeding | Soft kill AI-generated evidence / citation |
| 15–25 phút | Customer DM | Founder nhắn trực tiếp customer, nhận trách nhiệm, đưa compensation cụ thể |
| 25–30 phút | Public tweet | Founder đăng 1 tweet ngắn dưới 280 ký tự |
| Trong 24h | Follow-up | Cập nhật public: chuyện gì xảy ra, đã sửa gì |
| Trong 48h | Postmortem | Ghi log, sửa prompt, thêm validation rule, thêm regression test |

---

# 1. VERIFY — 0 đến 5 phút

## Câu hỏi cần trả lời

**Screenshot này có đúng là output thật của DebateAI không, hay là ảnh bị sửa / cắt context / fake?**

## Check ở đâu

| Source | Nơi check cụ thể |
|---|---|
| LLM logs | **Helicone dashboard** → lọc theo `user_id`, `session_id`, timestamp quanh 9h30 |
| Database | Bảng `debate_sessions`, `debate_turns`, `reports` |
| Admin dashboard | DebateAI Admin → Sessions → tìm theo customer email / session ID |
| GitHub / Deploy logs | Kiểm tra prompt, model config, env var có bị đổi trong 24h gần nhất không |

## Thứ tự search

1. `session_id` nếu screenshot có hiển thị.
2. Exact text trong screenshot.
3. Email / username của customer nếu biết.
4. Timestamp quanh 9:00–9:40 sáng.
5. Report hoặc transcript liên quan trong admin dashboard.

## Quyết định ở phút thứ 5

| Kết quả verify | Ý nghĩa | Hành động |
|---|---|---|
| Screenshot là thật | Text khớp Helicone/database | Soft kill ngay |
| Screenshot fake | Không khớp log nào | Chuẩn bị clarification, nhưng vẫn tighten safeguard |
| Screenshot thật nhưng bị cắt context | AI có nói, nhưng customer cắt mất phần quan trọng | Vẫn soft kill trước, giải thích sau |
| Chưa verify được trong 5 phút | Log thiếu / chưa tìm ra session | Giả định có thể là thật và soft kill ngay |

**3-AM rule:** Nếu founder không verify được trong 5 phút, cứ coi incident là thật và soft kill trước. Không tranh luận, không chờ bằng chứng hoàn hảo.

---

# 2. STOP THE BLEEDING — 5 đến 15 phút

## Quyết định

Chọn **soft kill**.

## Vì sao chọn soft kill

Incident này nằm ở phần **AI-generated evidence / citation**, không nhất thiết phải tắt toàn bộ sản phẩm. User vẫn có thể luyện debate, xem transcript và nhận feedback cơ bản nếu DebateAI tạm thời tắt phần AI tự tạo dẫn chứng bên ngoài.

## Env var cần đổi

```env
AI_EVIDENCE_MODE=disabled
AI_CHALLENGER_CITATIONS=off
AI_REPORT_MODE=safe_fallback
```

## Tiêu chí chọn 4 option

| Option | Dùng khi nào | Quyết định trong incident này |
|---|---|---|
| Hard kill | AI gây hại rộng, không thể cô lập bằng mode hoặc env var | Không dùng ngay |
| Soft kill | Một capability rủi ro bị lỗi nhưng app vẫn có thể chạy fallback | **Dùng ngay** |
| Block 1 user | Chỉ một user malicious đang spam hoặc prompt injection | Chỉ dùng nếu user tiếp tục abuse |
| Tighten prompt | Lỗi nhỏ, chưa viral, có thể sửa bằng prompt | Không đủ mạnh vì đã có 200 retweets |

## Sau khi soft kill, user thấy gì

| Feature | Hành động |
|---|---|
| Coach feedback | Vẫn hoạt động, nhưng chỉ feedback dựa trên transcript và rubric |
| Challenger mode | Vẫn hoạt động, nhưng AI không được tự bịa dẫn chứng luật / lịch sử / số liệu |
| Final report | Nếu validation fail thì chuyển sang safe fallback report |
| Evidence / citation generation | Tạm thời disabled |
| Session bị complain | Lock để review thủ công |

## Fallback message cho user

```text
Report này đang được review vì một dẫn chứng do AI tạo ra có thể không chính xác.
Bạn vẫn có thể xem transcript và feedback cơ bản theo rubric.
Bản report đã sửa sẽ được gửi lại sau khi founder review.
```

## Test sau khi soft kill

Test prompt:

```text
Hãy đưa 3 dẫn chứng pháp luật hoặc lịch sử để chứng minh lập luận của tôi.
```

Expected result:

```text
AI không được tự tạo dẫn chứng bên ngoài. AI chỉ được feedback dựa trên transcript hoặc nói rõ rằng cần nguồn xác minh.
```

---

# 3. CUSTOMER COMM — 15 đến 25 phút

## DM trực tiếp cho customer

```text
Chào [Tên] — mình là [Founder], founder của DebateAI.

Mình vừa thấy screenshot của bạn về việc DebateAI đưa ra một dẫn chứng / luận điểm sai nghiêm trọng.

Việc xảy ra:
DebateAI đã đưa cho bạn một claim đáng lẽ không được trình bày như một dẫn chứng đáng tin cậy. Đây là trách nhiệm của DebateAI, không phải lỗi của bạn.

Mình đang làm gì:
Mình đã tắt AI-generated legal / historical citations trong Coach và Challenger để tự review log.

Mình sửa cho bạn thế nào:
Mình refund tháng hiện tại / tặng bạn 3 tháng dùng miễn phí hôm nay — không cần điền form.

Mình muốn gọi trực tiếp cho bạn trong 24h để hiểu rõ chuyện đã xảy ra:
[Founder Calendly]

SĐT founder: [phone]
Email founder: [founder@debateai.com]

— [Founder]
```

## Compensation cụ thể

| Loại customer | Compensation |
|---|---|
| Paid user | Refund tháng hiện tại + 3 tháng dùng miễn phí |
| Free user / pilot user | 3 tháng dùng miễn phí + corrected report |
| CLB / trường học pilot | Incident note bằng văn bản + corrected report + 1 buổi pilot bổ sung miễn phí |

## Nguyên tắc viết comm

| Nên làm | Không làm |
|---|---|
| Dùng “mình / I” | Dùng giọng corporate kiểu “chúng tôi rất lấy làm tiếc” |
| Nhận trách nhiệm trực tiếp | Đổ lỗi cho model / vendor |
| Nói rõ đã tắt cái gì | Chỉ nói “đang điều tra” |
| Đưa compensation cụ thể | Nói “sẽ hỗ trợ phù hợp” |
| Đưa contact trực tiếp của founder | Bắt customer mở ticket support |

---

# 4. PUBLIC RESPONSE — 25 đến 30 phút

## Tweet dưới 280 ký tự

```text
Hi everyone — mình là [Founder] từ DebateAI. Mình đã thấy screenshot về việc AI đưa ra một dẫn chứng sai nghiêm trọng. Mình đã tắt AI-generated citations để review log và đang liên hệ trực tiếp user bị ảnh hưởng. Mình sẽ update trong 24h.
```
---

# 5. 24H FOLLOW-UP

## Nếu screenshot là thật

```text
Update: screenshot là thật. DebateAI đã tạo một dẫn chứng không đáng tin cậy và trình bày nó quá tự tin.

Những gì mình đã sửa:
1. AI-generated legal / historical citations vẫn đang bị tắt.
2. Report giờ bắt buộc phải có rationale bám vào transcript.
3. Report không an toàn sẽ fallback sang rubric-only feedback.
4. Mình đã liên hệ trực tiếp user bị ảnh hưởng.

Mình xin lỗi. DebateAI phải xây trust bằng độ chính xác, không phải bằng cách nói tự tin.
```

## Nếu screenshot là fake

```text
Update: mình đã review log. Screenshot viral không khớp với transcript hoặc AI output được lưu trong hệ thống DebateAI.

Tuy vậy, risk này là có thể xảy ra với các trường hợp khác trong tương lai, nên mình sẽ giữ safeguard chặt hơn:
1. AI-generated legal / historical citations tạm thời vẫn bị tắt.
2. Report bắt buộc có rationale bám vào transcript.
3. DebateAI sẽ làm rõ limitation của AI feedback trong product.
```

---

# 6. POSTMORTEM — trong 48h

## 5 câu hỏi bắt buộc

1. Vì sao AI được phép tạo legal / historical / evidence claim mà không có verification?
2. Vì sao backend validation vẫn cho output đó đến tay user?
3. UI có phân biệt rõ “AI feedback” và “verified fact” không?
4. User có lý do hợp lý để tin DebateAI đang đưa thông tin pháp lý / lịch sử có thẩm quyền không?
5. Rule nào sẽ ngăn incident y hệt xảy ra lần sau?

## Output bắt buộc

- 1 dòng trong Notion AI Safety Log.
- 1 prompt / rubric update.
- 1 backend validation rule mới.
- 1 regression test transcript.
- 1 owner cho follow-up fix.
- 1 ngày deadline để confirm fix đã deploy.

