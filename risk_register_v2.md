# risk_register_v2.md

# DebateAI Risk Register v2 — AI-Augmented CRO Audit

**Startup:** DebateAI  
**Stage:** Seed-stage / MVP  
**Team size:** 5 người  
**Runway basis:** Base scenario from Day 18 financial model  
**Monthly fixed cost:** 75,000,000 VND / tháng  
**Initial cash:** 1,200,000,000 VND  
**Base runway:** 16 tháng  
**Owner:** Founder  
**Last updated:** 07/05/2026  

---

## 0. Context

DebateAI là nền tảng luyện tranh biện với 2 core mode:

- **Challenge mode:** AI opponent tranh luận với user để user phát hiện điểm yếu trong lập luận.
- **Coach mode:** AI góp ý từng luận điểm để user cải thiện claim, reasoning, example và rebuttal.

Core product risk không chỉ là “AI trả lời sai”, mà là **user tin feedback sai và luyện sai hướng**. Với DebateAI, trust vào feedback/report là trust vào sản phẩm.

---

## 1. Runway Conversion

| Metric | Base |
|---|---:|
| Fixed cost / tháng | 75,000,000 VND |
| Initial cash | 1,200,000,000 VND |
| Base runway | 16 tháng |

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

> Tất cả impact trong file này đo bằng **tháng runway mất**, không đo bằng tiền hoặc % user.

---

## 2. Scoring Rule

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

# 3. Top 10 Risks

## RISK 1: AI Report Hallucination

- **Type:** Customer-facing
- **Affected feature:** Coach report, Challenger report, readiness score, next practice plan

### If

If AI Coach hoặc AI Challenger hallucinate feedback, chấm sai điểm, bịa lỗi lập luận, hoặc đưa next practice plan không khớp transcript,

### Then

Then user tin rằng mình yếu ở điểm không đúng, luyện sai hướng, screenshot report sai và nói public rằng DebateAI “AI chấm điểm bịa”.

### Leading to

Leading to khoảng **4 tháng runway mất** vì DebateAI phải pause pilot, refund/free credit cho user bị ảnh hưởng, sửa report pipeline và rebuild trust với CLB/trường học/early users.

### Likelihood

**4/5** — Khả năng cao vì report AI là core flow, transcript dài và nhiều tiêu chí Content / Style / Strategy dễ khiến model feedback generic hoặc suy luận sai.

### Impact

**4/5** — 3–6 tháng runway vì risk này đánh trực tiếp vào core trust của DebateAI.

### Mitigation

1. Dùng Pydantic validation để reject report thiếu `dimensionRationales`, `turnImpact`, `readinessReason`.
2. Không publish final report nếu AI không reference được turn cụ thể trong transcript.
3. Lưu 10 transcript mẫu làm regression test sau mỗi prompt update.

**Estimated cost:** $0–50/tháng  
**Score:** 16 — **KILL ZONE**

---

## RISK 2: False Legal/Historical Citation

- **Type:** Customer-facing
- **Affected feature:** Challenger evidence, Coach feedback, final report

### If

If AI tự tạo dẫn chứng về luật, lịch sử hoặc số liệu nhưng dẫn chứng đó sai nghiêm trọng hoặc xuyên tạc sự kiện,

### Then

Then user screenshot output và tố DebateAI lan truyền thông tin sai, khiến sản phẩm bị xem là nguy hiểm trong môi trường học thuật.

### Leading to

Leading to khoảng **5 tháng runway mất** vì founder phải tắt citation feature, xử lý public response, sửa prompt/guardrail, và delay partnership với CLB/trường học.

### Likelihood

**4/5** — DebateAI có domain tranh biện, nơi user thường yêu cầu evidence, luật, lịch sử, ví dụ xã hội. LLM rất dễ nói quá tự tin nếu không có retrieval/verification.

### Impact

**4/5** — 3–6 tháng runway vì ảnh hưởng trực tiếp đến trust, học thuật và partnership.

### Mitigation

1. Tắt AI-generated legal/historical citation trong MVP nếu không có retrieval verified.
2. Thêm rule: “AI chỉ được nói evidence là suggestion, không được trình bày như fact verified.”
3. Thêm safe fallback: nếu user hỏi dẫn chứng, AI hướng dẫn cách tìm nguồn thay vì bịa nguồn.

**Estimated cost:** $0–100/tháng  
**Score:** 16 — **KILL ZONE**

---

## RISK 3: OpenAI Quota Spike

- **Type:** Vendor
- **Vendor:** OpenAI API
- **Affected feature:** Coach mode, Challenger mode, final report generation

### If

If DebateAI tổ chức pilot với CLB tranh biện và 50 users cùng tạo session/report trong 1 giờ, khiến OpenAI API bị rate limit hoặc queue timeout,

### Then

Then users hoàn thành debate nhưng không nhận được report, session treo ở trạng thái “AI is generating feedback”, founder phải apology và recover report thủ công.

### Leading to

Leading to khoảng **2 tháng runway mất** vì team phải hotfix retry queue, thêm fallback, compensate early users và delay roadmap 1–2 tuần.

### Likelihood

**3/5** — Trung bình. MVP chưa có traffic lớn liên tục, nhưng pilot/workshop có thể tạo spike đột ngột.

### Impact

**2/5** — 1–2 tháng runway nếu xử lý nhanh.

### Mitigation

1. Thêm retry queue và timeout 60 giây cho report generation.
2. Giới hạn concurrent sessions trong pilot đầu tiên.
3. Log latency/error qua Helicone để phân biệt lỗi OpenAI vs backend.

**Estimated cost:** $0–50/tháng  
**Score:** 6 — Watch / Mitigate

---

## RISK 4: OpenAI Pricing Shock

- **Type:** Vendor
- **Vendor:** OpenAI API
- **Affected area:** Unit economics, COGS, pricing model

### If

If DebateAI dùng GPT-4/5-class model cho nhiều turn debate + structured report dài, và OpenAI pricing hoặc token usage thực tế cao hơn forecast,

### Then

Then COGS/khách vượt Base scenario, mỗi active user càng dùng nhiều thì startup càng burn nhanh, forcing founder phải cắt session limit hoặc tăng giá sớm.

### Leading to

Leading to khoảng **3 tháng runway mất** vì unit economics xấu, roadmap phải chuyển sang cost optimization, và growth test bị delay.

### Likelihood

**4/5** — Cao, vì PRD đã chấp nhận trade-off latency/cost cao hơn để có reasoning tốt, trong khi debate transcript nhiều turn dễ tốn token.

### Impact

**3/5** — Khoảng 3 tháng runway do cost optimization và pricing reset.

### Mitigation

1. Đặt token cap cho mỗi turn và mỗi final report.
2. Tóm tắt transcript trước khi generate report thay vì gửi full transcript.
3. Dùng cheaper model cho draft feedback, GPT-4/5-class chỉ dùng cho final reasoning.

**Estimated cost:** $0–100/tháng  
**Score:** 12 — Watch / Mitigate

---

## RISK 5: Vendor ToS Shift

- **Type:** Vendor
- **Vendor:** OpenAI / Anthropic / Google
- **Affected feature:** Debate topics, sensitive content, education use cases

### If

If LLM vendor cập nhật ToS hoặc safety policy làm hạn chế các chủ đề chính trị, luật, xã hội, chiến tranh, lịch sử hoặc sensitive debate topics,

### Then

Then Challenge mode trở nên yếu, né clash, từ chối nhiều topic hợp lệ, khiến user không còn thấy opponent đủ “khó”.

### Leading to

Leading to khoảng **3 tháng runway mất** vì core value “AI opponent đủ khó” bị giảm, founder phải rewrite prompt, thêm provider dự phòng và giải thích với early users.

### Likelihood

**3/5** — Trung bình. Vendor policy thay đổi không xảy ra hàng tuần, nhưng debate product phụ thuộc nhiều vào các chủ đề nhạy cảm.

### Impact

**3/5** — Khoảng 3 tháng runway do rework core mode.

### Mitigation

1. Chuẩn bị provider fallback: Anthropic Claude API hoặc Gemini API.
2. Tạo topic taxonomy: safe / sensitive / blocked để app kiểm soát trước khi gọi model.
3. Viết fallback UX: “topic này cần framing lại để luyện debate an toàn.”

**Estimated cost:** $0–150/tháng  
**Score:** 9 — Watch / Mitigate

---

## RISK 6: Founder Incident Bottleneck

- **Type:** Founder-bandwidth
- **Affected area:** Incident response, customer comm, prompt hotfix, runtime switch

### If

If founder hoặc tech lead bị ốm, bận thi cử, đi công tác hoặc mất liên lạc 3 ngày đúng lúc AI report bị lỗi và user complain public,

### Then

Then team không biết ai có quyền tắt AI mode, ai check Helicone log, ai reply customer, ai update prompt, và incident kéo dài quá 24–48h.

### Leading to

Leading to khoảng **3 tháng runway mất** vì incident không được contain trong giờ đầu, complaint lan rộng, roadmap delay và early users mất niềm tin vào team.

### Likelihood

**4/5** — Cao với team 5 người vì founder thường nắm product context, customer context và quyền ra quyết định.

### Impact

**3/5** — Khoảng 3 tháng runway nếu chưa có backup owner/playbook.

### Mitigation

1. Viết `incident_playbook.md` 1 trang, có 30-second checklist.
2. Chỉ định backup incident owner: Tech Lead.
3. Pin Helicone/Admin/OpenAI/GitHub/deploy links trong Slack/Discord nội bộ.

**Estimated cost:** $0/tháng  
**Score:** 12 — Watch / Mitigate

---

## RISK 7: GDPR/Data Deletion Gap

- **Type:** Regulatory
- **Affected data:** Email, debate transcript, report history, progress tracking, personalized weakness data

### If

If DebateAI lưu transcript, report history, progress tracking hoặc personalized weakness detection nhưng chưa có data deletion/export flow,

### Then

Then user, CLB hoặc partner trường học yêu cầu xoá dữ liệu nhưng team không thể xử lý rõ ràng, làm pilot bị pause hoặc mất partnership.

### Leading to

Leading to khoảng **4 tháng runway mất** vì team phải dừng growth để sửa data model, viết privacy flow, xoá dữ liệu thủ công và rebuild partner trust.

### Likelihood

**3/5** — Trung bình ở MVP, nhưng tăng nhanh khi có session history, progress tracking và personalization.

### Impact

**4/5** — 3–6 tháng runway nếu partner trường học hoặc user nghiêm túc về privacy.

### Mitigation

1. Thêm data deletion request flow đơn giản qua form/email founder.
2. Tạo admin action: delete user transcripts + reports trong 1 lần.
3. Viết privacy note rõ: DebateAI lưu gì, dùng để làm gì, xoá như thế nào.

**Estimated cost:** $0–50/tháng  
**Score:** 12 — Watch / Mitigate

---

## RISK 8: Prompt Injection Viral

- **Type:** Reputational
- **Affected feature:** Challenger mode, Coach mode, public demo

### If

If user cố tình prompt-inject Challenger để AI bỏ role, công kích người dùng, nói claim độc hại, hoặc tự nhận “DebateAI luôn đúng”,

### Then

Then user screenshot output và post rằng DebateAI toxic / biased / broken, làm founder phải pause demo hoặc pilot.

### Leading to

Leading to khoảng **3 tháng runway mất** vì launch bị chậm, founder phải xử lý public response, tighten prompt và sửa demo guardrail.

### Likelihood

**4/5** — Cao vì debate app khuyến khích adversarial interaction; user sẽ thử phá AI như một phần trải nghiệm.

### Impact

**3/5** — Khoảng 3 tháng runway nếu viral trong giai đoạn đang tìm early trust.

### Mitigation

1. Thêm prompt injection test suite 20 cases trước mỗi release.
2. Tắt public demo topics quá nhạy cảm nếu chưa có guardrail.
3. Log và rate-limit user liên tục cố tình jailbreak.

**Estimated cost:** $0–50/tháng  
**Score:** 12 — Watch / Mitigate

---

## RISK 9: Auth Failure During Pilot

- **Type:** Customer-facing
- **Affected feature:** Login, dashboard, session history, final report access

### If

If Google OAuth/custom auth lỗi trong ngày demo hoặc CLB pilot, khiến users không login được, không xem được report hoặc mất session history,

### Then

Then pilot conversion giảm, users nghĩ product chưa ổn định, founder phải reschedule demo hoặc gửi report thủ công.

### Leading to

Leading to khoảng **1 tháng runway mất** vì mất momentum pilot, delay feedback loop và tốn thời gian manual support.

### Likelihood

**3/5** — Trung bình. Auth issue không phải core AI risk nhưng rất dễ phá demo/pilot nếu app còn MVP.

### Impact

**2/5** — 1–2 tháng runway nếu xảy ra đúng ngày pilot.

### Mitigation

1. Có demo mode không cần login cho workshop/pilot.
2. Có fallback magic link hoặc guest session.
3. Trước pilot 24h chạy checklist: login, create session, complete report, view history.

**Estimated cost:** $0–50/tháng  
**Score:** 6 — Watch / Mitigate

---

## RISK 10: Progress Score Misread

- **Type:** Reputational
- **Affected feature:** Structured scoring, progress tracking, personalized weakness detection

### If

If DebateAI hiển thị readiness score, weakness detection hoặc improvement trends mà không giải thích baseline/uncertainty,

### Then

Then user hiểu nhầm điểm số là đánh giá năng lực tuyệt đối, phản ứng tiêu cực khi bị chấm thấp, hoặc tố sản phẩm “AI judge unfair”.

### Leading to

Leading to khoảng **2 tháng runway mất** vì founder phải redesign report explanation, xử lý support complaint và sửa scoring UX.

### Likelihood

**4/5** — Cao khi roadmap Next/Later có structured scoring, progress tracking và personalized weakness detection.

### Impact

**2/5** — 1–2 tháng runway; không chết ngay nhưng làm giảm trust và retention.

### Mitigation

1. Thêm label: “Score này chỉ dựa trên session hiện tại, không phải năng lực tuyệt đối.”
2. Hiển thị rationale theo từng dimension thay vì chỉ số tổng.
3. Cho user xem “next practice action” thay vì nhấn mạnh điểm thấp.

**Estimated cost:** $0/tháng  
**Score:** 8 — Watch / Mitigate

---

# 4. Summary Table

| Risk | Type | Runway lost | Likelihood | Impact | Score | Status |
|---|---|---:|---:|---:|---:|---|
| R1 — AI Report Hallucination | Customer-facing | 4 tháng | 4 | 4 | 16 | **KILL ZONE** |
| R2 — False Legal/Historical Citation | Customer-facing | 5 tháng | 4 | 4 | 16 | **KILL ZONE** |
| R3 — OpenAI Quota Spike | Vendor | 2 tháng | 3 | 2 | 6 | Watch |
| R4 — OpenAI Pricing Shock | Vendor | 3 tháng | 4 | 3 | 12 | Watch |
| R5 — Vendor ToS Shift | Vendor | 3 tháng | 3 | 3 | 9 | Watch |
| R6 — Founder Incident Bottleneck | Founder-bandwidth | 3 tháng | 4 | 3 | 12 | Watch |
| R7 — GDPR/Data Deletion Gap | Regulatory | 4 tháng | 3 | 4 | 12 | Watch |
| R8 — Prompt Injection Viral | Reputational | 3 tháng | 4 | 3 | 12 | Watch |
| R9 — Auth Failure During Pilot | Customer-facing | 1 tháng | 3 | 2 | 6 | Watch |
| R10 — Progress Score Misread | Reputational | 2 tháng | 4 | 2 | 8 | Watch |

---

# 5. Top 5 Priorities

## Priority 1 — AI Report Hallucination

**Why:** Core trust risk. If users do not trust feedback, DebateAI loses its main value.

**This week:**
1. Add report schema validation.
2. Require transcript-grounded rationale.
3. Create regression test set from 10 transcripts.

---

## Priority 2 — False Legal/Historical Citation

**Why:** Can become viral and damage academic trust.

**This week:**
1. Disable AI-generated legal/historical citations by default.
2. Add safe citation fallback.
3. Add warning label for unverified evidence suggestions.

---

## Priority 3 — Founder Incident Bottleneck

**Why:** Incident response cannot depend on one person.

**This week:**
1. Finalize 1-page `incident_playbook.md`.
2. Name Tech Lead as backup owner.
3. Pin emergency dashboard links.

---

## Priority 4 — GDPR/Data Deletion Gap

**Why:** Progress tracking and history make data retention a real risk.

**This week:**
1. Add manual deletion request flow.
2. Create admin deletion checklist.
3. Add privacy note in onboarding/settings.

---

## Priority 5 — OpenAI Pricing Shock

**Why:** Long debate transcripts can break unit economics.

**This week:**
1. Add token cap.
2. Summarize transcript before final report.
3. Track cost/session in dashboard or logs.

---

# 6. AI-Augmentation Evidence

## Risks from Workshop 2 already captured

| Existing risk | Kept in v2 as |
|---|---|
| OpenAI quota hit | R3 — OpenAI Quota Spike |
| AI Coach gives wrong feedback | R1 — AI Report Hallucination |
| Founder unavailable | R6 — Founder Incident Bottleneck |

## Risks AI/CRO audit added

| Added risk | Why it was missing before |
|---|---|
| False legal/historical citation | Workshop 2 focused on report hallucination, but did not separate evidence/citation risk |
| OpenAI pricing shock | Cost risk was mentioned as blindspot but not scored |
| Vendor ToS shift | Vendor dependency is not only downtime; policy changes can weaken debate topics |
| GDPR/data deletion gap | Regulatory risk appears once progress tracking/session history exists |
| Prompt injection viral | Debate product is naturally adversarial, so jailbreak risk is higher than normal chatbot |
| Auth failure during pilot | Non-AI failure can still kill pilot trust |
| Progress score misread | Structured scoring can be misunderstood as absolute judgment |

---

# 7. Pass/Fail Self-check

| Requirement | Status |
|---|---|
| Có ≥ 10 risks | Pass |
| Cover cả 5 type | Pass — Vendor, Customer-facing, Founder-bandwidth, Regulatory, Reputational |
| Mỗi risk theo If–Then–Leading to | Pass |
| Impact đo bằng tháng runway | Pass |
| Có ≥ 2 risks AI/CRO audit tìm ra mà Workshop 2 chưa có | Pass |
| Top 5 có mitigation founder-implementable trong 1 tuần | Pass |
| Mitigation cost < $500/tháng | Pass |
| Có ít nhất 1 regulatory risk | Pass — GDPR/Data Deletion Gap |

---

# 8. Final CRO Verdict

DebateAI không chết vì thiếu feature. DebateAI có khả năng chết vì **trust collapse**.

3 risk nguy hiểm nhất là:

1. AI report chấm sai nhưng nói như chắc chắn đúng.
2. AI bịa dẫn chứng luật/lịch sử rồi bị screenshot viral.
3. Founder/team không contain incident trong giờ đầu.

Nếu tuần này chỉ làm 3 việc, hãy làm:

1. **Disable unverified AI-generated citations.**
2. **Validate every final report against transcript-grounded schema.**
3. **Make incident response executable by Tech Lead, not only founder.**
