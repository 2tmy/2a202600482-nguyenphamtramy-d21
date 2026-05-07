# rules_rails_ritual.md

# AI Safety Rules — DebateAI v1

**Last updated:** 07/05/2026  
**Owner:** Founder  
**Startup:** DebateAI — AI Coach và AI Challenger cho luyện tranh biện

---

## 1. Biggest Risk

**Risk lớn nhất:**  
AI Coach hoặc AI Challenger tạo report sai nhưng viết như chắc chắn đúng: chấm sai điểm, bịa lỗi lập luận, bịa dẫn chứng, hoặc đưa next practice plan không khớp transcript.

**Why this matters:**  
DebateAI bán trust vào feedback. Nếu user nhận một report sai, họ không chỉ bỏ app mà còn có thể screenshot public rằng DebateAI “AI chấm điểm bịa”. Với startup nhỏ, mất trust ở report = mất core product.

---

## 2. RULES

| Rule line | Rule |
|---|---|
| Cấm cụ thể | **KHÔNG paste transcript DebateAI, email user, session ID, report lỗi, API key hoặc feedback thật vào ChatGPT Free/Plus, Claude Free/Pro, Gemini public hoặc Poe.** |
| Allowed alternative | **DÙNG OpenAI API qua backend DebateAI + Helicone logging** để generate/debug feedback. Nếu cần debug thủ công, chỉ dùng transcript đã anonymize qua internal admin flow. Cost dự kiến: OpenAI API **~$100/tháng**, Helicone **$0/tháng** ở MVP stage. |
| Hậu quả vi phạm | Lỗi vô ý lần 1: founder talk 1-1 trong 24h, ghi vào Notion AI Safety Log. Lỗi vô ý lần 2: remove quyền access production transcript trong 2 tuần. Cố tình bypass backend, paste customer data vào public LLM, hoặc che giấu incident: let go. |
| Update mechanism | Rules được update tại **[DebateAI AI Safety Rules — Notion Link]**. Founder update sau mỗi incident, mỗi lần launch mode mới, hoặc sau Friday Report Accuracy Review. |

---

## 3. RAILS

| Rail | Vendor / Tool | Chặn risk như thế nào | Cost / month |
|---|---|---|---:|
| LLM observability | **Helicone** | Log toàn bộ prompt/response từ OpenAI API. Khi user complain report sai hoặc screenshot viral, founder có thể verify session thật trong 5 phút. | **$0** free tier |
| Report schema validation | **Pydantic — FastAPI backend** | Reject AI report nếu thiếu field bắt buộc, score ngoài range, thiếu rationale, hoặc feedback không map với transcript turn. Không cho report lỗi đi thẳng tới user. | **$0** |
| AI generation vendor | **OpenAI API** | Chỉ backend DebateAI được gọi model. Không cho team generate final report bằng ChatGPT public. | **~$100/tháng** MVP usage |

**Total RAILS cost:** **~$100/tháng**  
**Budget check:** dưới $500/tháng.

---

## 4. RITUAL

# Friday 30' Report Accuracy Review

**Frequency:** Mỗi thứ Sáu  
**Owner:** Founder + Tech Lead  
**Duration:** 30 phút  
**Input:**  
- 5 report Coach/Challenger gần nhất  
- 1 report có score thấp nhất trong tuần  
- mọi user feedback / bug report liên quan đến AI feedback  

---

## Founder question

> “Trong tuần này, có report nào khiến user hiểu sai họ cần cải thiện gì không? Nếu có, câu feedback nào sai nhất, transcript turn nào chứng minh nó sai, và vì sao backend vẫn cho report đó pass?”

---

## Steps

1. Founder mở admin dashboard hoặc report history.
2. Chọn:
   - 2 Coach reports gần nhất
   - 2 Challenger reports gần nhất
   - 1 report có score thấp nhất hoặc bị user complain
3. Với mỗi report, check 4 câu:
   - Feedback có quote/reference đúng turn trong transcript không?
   - Score có rationale cụ thể không?
   - Có câu nào nghe chắc chắn nhưng không có evidence không?
   - Next practice plan có actionable trong 1 buổi luyện không?
4. Nếu phát hiện report lỗi:
   - ghi lỗi vào Notion AI Safety Log
   - tag lỗi: hallucination / generic feedback / wrong score / missing rationale
   - Tech Lead thêm hoặc sửa Pydantic validation nếu lỗi có pattern
   - Founder hoặc Tech Lead update prompt qua GitHub PR, bắt buộc 1 reviewer approve

---

## Output mỗi tuần

- 1 dòng trong Notion AI Safety Log
- 1 prompt/rubric improvement nếu cần
- 1 validation rule mới nếu lỗi có pattern
- 1 report example được lưu làm regression test

---

## 5. Self-check

| Question | Answer |
|---|---|
| Tổng cost RAILS dưới $500/tháng? | **Có.** Tổng khoảng **$100/tháng** ở MVP stage. |
| RITUAL implement được trong 1 tuần? | **Có.** Dùng report history/admin dashboard + Notion + GitHub PR, không cần hire compliance officer. |