# DebateAI Risk Register — Workshop 2

**Startup:** DebateAI  
**Product:** Nền tảng luyện tranh biện với AI Coach và AI Challenger  
**Stage:** MVP / Seed-stage  
**Team size:** 5 người  
**Owner:** Founder  
**Last updated:** 07/05/2026  
**Output file:** `risk_register.md`

---

## 0. Runway Conversion

**Scenario used:** Base scenario from Day 18 financial model.

| Metric | Base |
|---|---:|
| Fixed cost / tháng | 75,000,000 VND |
| Initial cash | 1,200,000,000 VND |
| Base runway | 16 tháng |

**Formula:**

```text
Runway = Initial cash / Monthly fixed cost
Runway = 1,200,000,000 / 75,000,000 = 16 tháng
```

## Quy đổi incident cost sang tháng runway

| Incident cost | Runway lost |
|---:|---:|
| 5,000,000 VND | 0.07 tháng |
| 50,000,000 VND | 0.67 tháng |
| 75,000,000 VND | 1 tháng |
| 150,000,000 VND | 2 tháng |
| 225,000,000 VND | 3 tháng |
| 300,000,000 VND | 4 tháng |
| 450,000,000 VND | 6 tháng |
| 500,000,000 VND | 6.67 tháng |

> Risk trong file này được đo bằng **tháng runway mất**, không đo bằng tiền hoặc % user.

---

## 1. Scoring Rule

| Runway lost | Impact score |
|---|---:|
| < 1 tháng | 1 |
| 1–2 tháng | 2 |
| 3 tháng | 3 |
| 3–6 tháng | 4 |
| > 6 tháng | 5 |

**Score = Likelihood × Impact**

| Score | Meaning |
|---:|---|
| 1–4 | Accept |
| 5–14 | Watch / Mitigate |
| 15–25 | KILL ZONE |

---

# 2. Top 3 Risks

## Risk 1 — OpenAI Quota Hit During Debate Workshop

**Type:** Vendor risk  
**Vendor:** OpenAI API  
**Risk pattern:** Replika-style vendor dependency  
**Affected feature:** Coach mode, Challenger mode, final report generation

### If

If DebateAI tổ chức pilot với CLB tranh biện hoặc nhóm sinh viên và 50 users cùng tạo Coach / Challenger sessions trong 1 giờ, khiến OpenAI API bị rate limit, latency tăng mạnh hoặc report generation queue timeout,

### Then

Then nhiều users hoàn thành debate nhưng không nhận được final report, session bị treo ở trạng thái “AI is generating feedback”, và founder phải xử lý apology, free credit hoặc manual report recovery cho nhóm early users.

### Leading to

Leading to khoảng **2 tháng runway mất** vì team phải:

- hotfix retry queue,
- thêm fallback model,
- recover report thủ công cho user bị lỗi,
- delay roadmap 1–2 tuần,
- compensate early users bằng free credit hoặc extended trial.

### Score

| Dimension | Score | Reasoning |
|---|---:|---|
| Likelihood | 3 | Khả năng trung bình. DebateAI phụ thuộc OpenAI API, đặc biệt khi có nhiều session/report chạy cùng lúc trong workshop hoặc pilot. |
| Impact | 2 | Khoảng 1–2 tháng runway mất. Sự cố gây downtime và trust loss, nhưng chưa phá trực tiếp core positioning nếu xử lý nhanh. |
| Total score | **6** | Watch / Mitigate |

### Mitigation

- Thêm retry queue cho report generation.
- Thêm timeout rõ ràng: nếu AI report quá 60 giây, trả fallback message và gửi report sau.
- Chuẩn bị fallback provider: Anthropic Claude API hoặc Gemini API.
- Log latency/error qua Helicone để biết lỗi đến từ OpenAI, backend hay prompt.
- Giới hạn số session đồng thời trong pilot đầu tiên để tránh spike.

---

## Risk 2 — AI Coach Gives Wrong Feedback as If It Is True

**Type:** Customer-facing AI risk  
**Risk pattern:** Air Canada-style hallucinated output  
**Affected feature:** Coach report, Challenger report, readiness score, next practice plan

### If

If AI Coach hoặc AI Challenger hallucinate feedback, chấm sai điểm, bịa lỗi lập luận, bịa điểm mạnh/yếu, hoặc đưa next practice plan không khớp transcript,

### Then

Then user tin rằng mình yếu ở điểm không đúng, luyện sai hướng, screenshot report sai và nói public rằng DebateAI “AI chấm điểm bịa”.

### Leading to

Leading to khoảng **4 tháng runway mất** vì DebateAI phải:

- pause pilot với CLB / trường học / early partners,
- refund hoặc tặng free credit cho nhóm user bị ảnh hưởng,
- dừng roadmap để sửa report pipeline,
- review lại prompt, rubric và validation logic,
- rebuild trust với early users.

### Score

| Dimension | Score | Reasoning |
|---|---:|---|
| Likelihood | 4 | Khả năng cao vì report AI là core flow. Transcript dài, nhiều turn và nhiều tiêu chí Content / Style / Strategy dễ khiến model feedback generic hoặc suy luận sai. |
| Impact | 4 | Mất khoảng 3–6 tháng runway vì trust vào core product bị phá vỡ. Nếu user không tin report, DebateAI mất giá trị chính. |
| Total score | **16** | **KILL ZONE** |

### Mitigation

- Backend bắt buộc report có `dimensionRationales`, `turnImpact`, `readinessReason`.
- Không cho AI publish final report nếu không reference được turn cụ thể trong transcript.
- Dùng Pydantic validation để reject report thiếu field, score ngoài range hoặc thiếu rationale.
- Nếu validation fail, trả safe fallback report thay vì report hallucinated.
- Log toàn bộ prompt/response qua Helicone để verify khi có complaint.
- Mỗi tuần review 5 report thật trong Friday Report Accuracy Review.
- Lưu 10 transcript mẫu làm regression test sau mỗi lần update prompt.

---

## Risk 3 — Founder Unavailable During Critical AI Incident

**Type:** Founder-bandwidth risk  
**Risk pattern:** Single point of failure  
**Affected area:** Incident response, prompt hotfix, customer communication, AI runtime switch

### If

If founder hoặc tech lead bị ốm, bận, thi cử, đi công tác hoặc mất liên lạc 3 ngày đúng lúc AI report bị lỗi và user complain public,

### Then

Then team không biết ai có quyền tắt AI mode, ai reply customer, ai check Helicone log, ai update prompt, ai đổi runtime sang fallback, và incident bị kéo dài quá 24–48h.

### Leading to

Leading to khoảng **3 tháng runway mất** vì:

- incident không được contain trong giờ đầu,
- customer complaint lan rộng,
- team mất 1–2 tuần xử lý khủng hoảng,
- roadmap bị delay,
- early users mất niềm tin vào khả năng phản ứng của team.

### Score

| Dimension | Score | Reasoning |
|---|---:|---|
| Likelihood | 4 | Khả năng cao ở startup 5 người vì founder thường giữ product context, customer context, prompt logic và quyền ra quyết định incident. |
| Impact | 3 | Khoảng 3 tháng runway mất. Sự cố nghiêm trọng nhưng có thể giảm impact nếu có playbook và backup owner. |
| Total score | **12** | Watch / Mitigate |

### Mitigation

- Viết `incident_playbook.md` 1 trang cho AI report incident.
- Chỉ định backup incident owner: Tech Lead.
- Tạo quyền truy cập sẵn cho Helicone, admin dashboard, OpenAI dashboard và deployment platform.
- Có env var `AI_REPORT_MODE=fallback` để soft kill report generation.
- Pin link emergency checklist trong Slack / Discord nội bộ.
- War game 30 phút mỗi tháng: giả lập “AI report sai + user screenshot public”.

---

# 3. 2x2 Risk Matrix

| Impact / Likelihood | Low Likelihood 1–2 | High Likelihood 3–5 |
|---|---|---|
| High Impact 4–5 | Watch | **Risk 2 — AI Coach gives wrong feedback** |
| Medium Impact 3 | Watch | Risk 3 — Founder unavailable during incident |
| Low Impact 1–2 | Accept | Risk 1 — OpenAI quota hit during debate workshop |

---

# 4. KILL ZONE

| Risk | Type | Runway lost | Likelihood | Impact | Score | Kill Zone? |
|---|---|---:|---:|---:|---:|---|
| Risk 1 — OpenAI Quota Hit During Debate Workshop | Vendor | 2 tháng | 3 | 2 | 6 | No |
| Risk 2 — AI Coach Gives Wrong Feedback as If It Is True | Customer-facing | 4 tháng | 4 | 4 | 16 | **Yes** |
| Risk 3 — Founder Unavailable During Critical AI Incident | Founder-bandwidth | 3 tháng | 4 | 3 | 12 | No |

---

# 5. Workshop 3 Priority

**Primary incident for Workshop 3:**  
AI Coach / Challenger tạo report sai, user screenshot public, có signal viral.

**Reason:**  
Đây là risk duy nhất nằm trong **KILL ZONE** với score **16**. Risk này đánh trực tiếp vào core trust của DebateAI: nếu user không tin AI feedback/report, sản phẩm mất giá trị chính.

---

# 6. Known Blindspots for Risk Register v2

Workshop 2 chỉ yêu cầu 3 risks từ 3 type khác nhau. Tuy nhiên, để chuẩn bị cho `risk_register_v2.md`, DebateAI cần bổ sung thêm các risk type sau:

| Missing type | Risk cần thêm ở v2 | Vì sao quan trọng |
|---|---|---|
| Regulatory | Transcript retention / data deletion / GDPR | DebateAI lưu transcript, report history và progress tracking. Nếu user yêu cầu xoá dữ liệu mà team chưa có flow, partnership có thể bị delay. |
| Reputational | Prompt injection screenshot viral | User có thể cố tình làm Challenger/Coach nói câu vô lý, sau đó screenshot public. |
| Cost / Unit economics | Long transcript làm API cost spike | Debate session dài + structured report nhiều field có thể khiến API cost vượt forecast. |
| Auth / Access | Login hoặc dashboard lỗi trong pilot | Nếu user không vào được session/report trong demo day, conversion và trust giảm mạnh. |

---

# 7. Pass/Fail Self-check

| Requirement | Status |
|---|---|
| Có 3 risks từ 3 type khác nhau | Pass |
| Có Vendor risk specific | Pass — OpenAI quota/rate limit trong debate workshop |
| Có Customer-facing AI risk | Pass — AI report hallucination |
| Có Founder-bandwidth risk | Pass — founder unavailable during incident |
| Mỗi risk theo If–Then–Leading to | Pass |
| Impact đo bằng tháng runway | Pass |
| Runway dựa trên Base scenario Day 18 | Pass |
| Likelihood realistic, không phải tất cả = 5 | Pass |
| Có ít nhất 1 risk ở KILL ZONE | Pass — Risk 2 |

---

# 8. Final Decision

Risk được chọn để đưa sang Workshop 3:

## AI Coach / Challenger tạo report sai, user screenshot public, có signal viral

Đây là risk quan trọng nhất vì:

- nằm trong **KILL ZONE**,
- có score cao nhất: **16**,
- đánh trực tiếp vào core trust của DebateAI,
- phù hợp nhất để viết `incident_playbook.md` ở Workshop 3.
