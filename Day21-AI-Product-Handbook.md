# Day 21 — Sổ tay học viên
## AI Governance & Risk
### Phanh Brembo cho startup AI

> **Big company governance = avoid lawsuit.**
> **Startup governance = avoid death.**

---

## 0. Cách dùng sổ tay này

Dùng **trong lúc làm 4 workshops** — không phải để đọc hết một lượt. Mỗi lần bí, mở đúng phần cần:

| Khi bạn cần… | Mở phần… |
|---|---|
| Hiểu mạch logic tổng thể | §1 |
| Đọc nhanh một khái niệm (3 R's / Risk Register / Incident...) | §2 |
| Hướng dẫn từng bước workshop | §3 |
| Chạy AI để augment risk discovery | §4 (Prompts) |
| Biết output gì cần có ở mỗi checkpoint | §5 (Checkpoints) |
| Xem tiêu chí chấm điểm & cách submit | §6 (Rubric & Submission) |
| Đọc tham khảo sâu hơn | §7 (References) |

**Quy ước ngôn ngữ:** Tiếng Việt ưu tiên. Các **term, công thức, prompt** giữ tiếng Anh để chuẩn ngành và giao tiếp tốt với AI.

---

## 1. Mạch logic Day 21

### Tại sao Day 21 quan trọng?

Day 16-20, các bạn học cách **thắng** — customer, PRD, unit economics, pitch, roadmap. Mindset: tăng tốc.

Hôm nay, Day 21, mở đầu Chương 5 — **học cách không chết**.

> Tôi đã thấy nhiều startup AI *thắng* 2 năm đầu rồi *chết* năm thứ 3. Một bug critical, một customer kiện, một viral incident — và 18 tháng work tan biến.

Day 21 đảm bảo các bạn không thuộc nhóm đó.

### Câu hỏi trung tâm

> **Làm sao để 1 sự cố AI không làm cạn runway của bạn?**

### Nguyên lý Brembo

```
Phanh Brembo trên Lamborghini không sinh ra để bạn đi chậm.
Nó sinh ra để bạn DÁM chạy 300 km/h — mà không sợ chết.
```

Áp dụng vào AI startup:

> **Governance không phải để giới hạn. Là điều kiện để dám scale.**

Một startup không có governance = siêu xe không phanh. Founder dám chạy 100 km/h — nhưng sẽ không bao giờ dám chạy 300.

### 4 cửa ải hôm nay

```
Cửa 1: 3 R's của governance (Rules / Rails / Ritual)
              ↓
Cửa 2: Risk Register theo tháng runway
              ↓
Cửa 3: Founder always-on-call playbook
              ↓
Cửa 4: AI Lab — augment risk discovery
              ↓
        4 file submission
        (rules_rails_ritual / risk_register / incident_playbook / risk_register_v2)
```

### 3 case studies & 3 framework

| Block | Case study | Năm | Lesson cốt lõi |
|---|---|---|---|
| **1. 3 R's** | Air Canada chatbot | 2024 | Chatbot = legally binding spokesperson từ ngày 1 |
| **2. Risk Register** | Replika user revolt | 2023 | Vendor risk + Communication risk = 2 killers |
| **3. Incident response** | DPD viral haiku | 2024 | Hour 1 quan trọng hơn hour 24 |

### Output cuối buổi

4 files markdown — bộ governance package để show với VC:
- `rules_rails_ritual.md`
- `risk_register.md`
- `incident_playbook.md`
- `risk_register_v2.md` (AI-augmented)

---

## 2. Các khái niệm chính

### 2.1 Big company governance vs Startup governance

Đây là mindset shift quan trọng nhất Day 21.

| | **Big company** | **Startup early-stage** |
|---|---|---|
| **Stake** | Tránh lawsuit, regulator fine | Tránh **death** (1 incident = mất runway) |
| **Mindset** | Compliance | Survival |
| **Audience pitch** | Board, regulators | Investor + customer |
| **Tool budget** | $50K+/năm | $0–500/tháng |
| **Speed** | Quarterly review | Friday 30' check |
| **Comm style** | Corporate statement, PR team | Founder personal voice |
| **Documentation** | 50-trang policy | 1-trang Notion |
| **Process** | Multi-stage approval | Founder DM Slack "OK" |

> **Bài học cốt lõi:** Đừng copy Stripe playbook. Stripe có 1000 engineers. Bạn có 5.

---

### 2.2 Air Canada precedent — Tại sao $812 quan trọng?

#### Tóm tắt case

- **11/2022:** Jake Moffatt cần bay Vancouver–Toronto cho đám tang bà nội
- Anh hỏi chatbot Air Canada về *bereavement fare* (giá vé tang sự)
- Chatbot **bịa** policy: "*Apply refund trong 90 ngày SAU chuyến bay*"
- Policy thật: phải apply **TRƯỚC** chuyến bay
- Air Canada từ chối refund → Moffatt kiện
- Defense Air Canada: *"Chatbot là legal entity riêng, công ty không chịu trách nhiệm"*

#### Phán quyết landmark — 14/2/2024

Tribunal Member Christopher C. Rivers (Moffatt v. Air Canada, 2024 BCCRT 149):

> *"This is a remarkable submission. While a chatbot has an interactive component, it is still just a part of Air Canada's website. It should be obvious to Air Canada that it is responsible for all the information on its website."*

**Air Canada phải trả $812.02 CAD** ($650.88 fare diff + $36.14 interest + $125 fees).

#### 4 nguyên tắc precedent thiết lập

| Nguyên tắc | Ý nghĩa |
|---|---|
| **Chatbot = phần của startup** | Không phải vendor riêng. Là bạn. |
| **Lời chatbot = hợp đồng implicit** | Customer đọc, tin, act → binding |
| **"AI bịa" không phải excuse** | Phải đảm bảo accuracy, không thể blame model |
| **Customer được quyền tin** | Không cần double-check với webpage khác |

#### Ý nghĩa với startup

> **Chatbot của bạn = legally binding spokesperson từ ngày 1.**

Không có grace period. Không có "em mới startup, đợi em scale". Ngày bạn launch chatbot = ngày bạn nhận trách nhiệm pháp lý cho mọi câu nó nói.

**Worst-case startup scenario:**
- 1 câu chatbot bịa
- 1000 customer tin
- Class action — mỗi customer claim $500
- Tổng: $500,000 = **10 tháng runway** (nếu burn $50K/tháng) = **end of runway**

Đây là tại sao phải có brake.

---

### 2.3 3 R's của startup governance

Framework lightweight thay cho Governance 4 tầng (Policy/Process/Tooling/People) của big company.

```
RULES   — 1 trang Notion. Founder viết. Update khi thay đổi.
RAILS   — Stack tech $0–500/tháng. Tự động chặn. Audit log.
RITUAL  — Hành vi founder + team. Friday 30' check. Customer Friday.
```

**Đặc điểm 3 R's:** lightweight, founder-led, implement trong **1 tuần**.

---

#### 2.3.1 R1 — RULES

> **1 trang Notion. Founder viết. Update khi thay đổi.**

##### Bad vs Good

| **❌ BAD: Corporate policy** | **✅ GOOD: 1-trang Notion startup** |
|---|---|
| 50 trang | 1 trang |
| Legal review | Founder viết |
| Quarterly update | Update khi thay đổi |
| "Cấm dùng AI sai mục đích" (cliché) | "KHÔNG paste customer chat vào ChatGPT public" (specific) |
| "Bảo vệ data công ty" (mơ hồ) | "DÙNG OpenAI Enterprise (đã setup) — data không train" (concrete) |
| "Vi phạm sẽ bị kỷ luật theo quy chế" | "Vi phạm → founder talk 1-1. Lần 2 → let go" |

##### Template RULES (sample)

```markdown
# AI Safety Rules — v1
[Last updated: DD/MM/YYYY by Founder]

## ❌ KHÔNG được làm
- Paste customer chat / source code / API keys / financial data
  vào ChatGPT public hoặc Claude public
- Share Notion docs có customer data với người ngoài team
- Deploy AI feature mới mà chưa pre-launch review

## ✅ Được làm (alternatives)
- DÙNG OpenAI Enterprise (đã setup, data không train)
  → Login: [link]
- DÙNG Cursor + Copilot trong IDE (đã setup)
  → Setup guide: [link]
- DÙNG Claude for Work cho long-form analysis
  → Login: [link]

## ⚠️ Hậu quả vi phạm
- Lần 1: Founder talk 1-1, ghi note
- Lần 2: Let go

## 📞 Câu hỏi?
- Slack #ai-safety hoặc DM [Founder]
```

##### 4 câu hỏi mọi RULES phải trả lời

1. **Cái gì cấm?** (Specific vendor + action)
2. **Cái gì được làm?** (Alternative tool + cost)
3. **Hậu quả vi phạm?** (Concrete, không "kỷ luật")
4. **Ai update?** (Founder, không Legal team)

> **Pro tip:** Founder *tự viết* bằng giọng của founder. Đừng download policy template từ Google — nhân viên detect ngay = không đọc.

---

#### 2.3.2 R2 — RAILS

> **Stack tech $0–500/tháng. Tự động chặn. Audit log.**

> *Don't trust humans to remember rules. Build cheap rails.*

##### Stack startup-friendly

| Mục tiêu | Tool | Cost |
|---|---|---|
| **Chặn paste data nhạy cảm vào public LLM** | NextDNS DNS filtering hoặc Chrome admin policy block | $0–40/tháng |
| **Cấp Enterprise LLM (data không train)** | OpenAI Enterprise hoặc Claude for Work | $25–60/user/tháng |
| **Chặn API key, secrets vào git** | `git-secrets` OSS hoặc pre-commit hooks | $0 |
| **Log mọi LLM prompt/response** | Helicone free tier (100K req/tháng) hoặc LangFuse OSS self-host | $0–50/tháng |
| **Audit ai dùng tool gì** | Google Workspace audit log + Notion log | $0 (đã có) |
| **Code review trước commit** | GitHub branch protection + 1 reviewer required | $0 (đã có) |

**Tổng stack startup 5-người:** dưới **$300/tháng**. Setup trong 1 ngày.

##### Setup priority order

Nếu budget hạn chế, làm theo thứ tự ưu tiên:

1. **Free tier first** (priority #1):
   - `git-secrets` OSS — chặn secrets vào git
   - Helicone free tier — log mọi LLM call
   - GitHub branch protection — code review

2. **Cheap paid** (priority #2):
   - NextDNS — block public LLM ($40/tháng)
   - OpenAI Enterprise — Enterprise tier cho team

3. **Optional** (priority #3):
   - LangFuse self-host — nếu cần audit deep
   - Custom DLP rules — nếu có data đặc biệt

> **So sánh:** enterprise stack (Symantec DLP, Zscaler, Okta, Palo Alto) tốn **$50K+/năm**. Startup không cần.

##### Vì sao R2 quan trọng nhất khi crisis

Khi viral incident xảy ra (giống DPD):
- **Verify nhanh:** check log Helicone trong 5 phút → biết đó có thật là AI của mình không
- **Block 1 user:** identify user gây ra crisis qua audit log
- **Tighten prompt:** deploy prompt update qua Git pipeline

Không có R2 = không respond được nhanh khi crisis.

---

#### 2.3.3 R3 — RITUAL

> **Hành vi founder + team. Cheap nhất nhưng quan trọng nhất.**

> *Rules là giấy. Rails là code. Ritual là behavior — thay đổi văn hóa.*

##### 5 rituals startup-realistic

| Ritual | Mô tả | Tần suất | Cost |
|---|---|---|---|
| **Friday 30' Risk Review** | Founder + tech lead nhìn lại tuần: hallucination? Customer complaint? Vendor đổi gì? | Mỗi tuần | 30' |
| **Customer Friday** | Founder gọi 1 customer/tuần: *"AI có sai bao giờ chưa? Lúc đó em làm gì?"* | Mỗi tuần | 30' |
| **Onboarding chat 15'** | Day 1 hire mới: founder kể 15' về AI safety + show Notion. Day 7: review prompts. | Per hire | 30' |
| **Pre-launch review** | Trước launch feature: 2 người review prompts + edge cases | Per feature | 30' |
| **War game** | Simulate incident: *"AI vừa nói khách bị ung thư, viral 500K views"* | Quarterly | 60' |

##### Tại sao Customer Friday powerful

Founder thường tránh gọi customer trực tiếp. Họ rely on NPS surveys, support tickets, dashboards.

Sự thật: customer nói thẳng nhất khi founder gọi trực tiếp. Họ sẽ cho biết những thứ NPS không capture:

- *"Tuần trước AI của bạn nói X — em phải gọi support sửa. Khó chịu lắm."*
- *"Có một lần AI bịa giá. Em xài tool khác để check."*
- *"Em đang nghĩ chuyển sang competitor vì AI này hay sai."*

Mỗi cuộc gọi 5-10 phút. Mỗi tuần 1 customer. Sau 6 tháng = 26 conversations với customer thật. Insight không thể buy được.

##### War game template

Quarterly, 1 giờ. Simulate scenario:

```
Tình huống: "Sáng thứ Hai. Customer của bạn livestream TikTok 50K viewers.
Họ vừa screenshot AI của bạn nói SAI một câu hoàn toàn về sản phẩm khách.
Đã có 200 retweets trong 30 phút."

Stopwatch start → team chạy playbook → time it → find gaps → update.
```

---

### 2.4 Risk Register theo tháng runway

Đo risk không bằng $ hay % users. Đo bằng **tháng runway còn lại sau incident**.

#### Vì sao "tháng runway"?

- **$50K với startup A** (burn $10K/tháng) = 5 tháng runway
- **$50K với startup B** (burn $50K/tháng) = 1 tháng runway

Cùng $50K. Mức độ nguy hiểm khác nhau.

> Đo bằng tháng runway = standardize across mọi startup. Dễ compare, dễ ưu tiên.

#### PR drama vs Survival risk

| **PR drama** (báo chí) | **Startup survival risk** (founder phải lo) |
|---|---|
| AI chatbot chửi bậy (DPD) | AI bịa policy → class action (Air Canada) |
| AI sinh deepfake | Vendor change đột ngột → user revolt (Replika) |
| AI bias chủng tộc | Prompt injection → viral PR (DPD) |
| AI nói dối lịch sử | OpenAI rate limit → app down |

| | PR drama | Survival risk |
|---|---|---|
| **Big company** | Tweet apology → fixed | Lawsuit → trả phạt |
| **Startup** | 50% MRR drop trong 1 tuần | $50K–500K = 3–12 tháng runway = chết |

> **Mindset shift:** Risk = financial survival, không phải PR moderation.

---

### 2.5 If-Then-Leading to formula

Risk Register chuẩn theo công thức 3 dòng:

```
If [cause]
Then [event]
Leading to [impact in tháng runway]
```

#### Bad vs Good

| **❌ BAD: Mơ hồ** | **✅ GOOD: Specific với runway** |
|---|---|
| "AI có thể trả lời sai." | **If** chatbot bịa policy về refund (như Air Canada),<br>**then** 10 customer claim refund + 1 lawsuit BCCRT,<br>**leading to** $15K legal + $5K refunds = **2 tháng runway**. |

> **Quy đổi mọi risk về tháng runway:** $5K = ?, $50K = ?, $500K = ? Phụ thuộc burn rate startup bạn.

---

### 2.6 5 risk types (cho startup AI)

Mỗi Risk Register phải cover **cả 5 type**:

| # | Type | Mô tả | Ví dụ |
|---|---|---|---|
| 1 | **Vendor** | OpenAI/Anthropic/Cloud thay đổi | Rate limit cut 10x, ToS update cấm sexual content (Replika) |
| 2 | **Customer-facing** | AI tương tác customer sai | Chatbot bịa policy (Air Canada), prompt injection |
| 3 | **Founder-bandwidth** | Founder ốm/bận, critical bug không fix | Founder du lịch 1 tuần, OpenAI rate limit hit, không ai handle |
| 4 | **Regulatory** | EU AI Act, VN Luật AI 2025, GDPR | EU AI Act phạt €35M cho high-risk AI không tuân thủ |
| 5 | **Reputational** | Viral incident gây brand damage | DPD haiku 1.7M views |

> **Founder thường chỉ lo Reputational (PR).** Quên 4 type còn lại — nguy hiểm hơn nhiều.

---

### 2.7 Likelihood × Impact scoring

Sau khi viết If-Then-Leading to → chấm 2 chiều:

- **Likelihood** (1-5): khả năng xảy ra trong 1 quý
- **Impact** (1-5): tháng runway mất

#### Quy đổi runway → Impact score

| Runway lost | Impact score |
|---|---:|
| <1 tháng | 1 |
| 1–2 tháng | 2 |
| 3 tháng | 3 |
| 3–6 tháng | 4 |
| >6 tháng | 5 |

#### KILL ZONE matrix

```
              Likelihood
          Low (1-2)    High (4-5)
        ┌─────────────┬──────────────┐
   High │   Watch     │  KILL ZONE   │
   (>3mo)│ Plan B sẵn │ Mitigate     │
        │             │  ngay tuần này│
   Imp. ├─────────────┼──────────────┤
   Low  │  Accept     │  Mitigate    │
   (<1mo)│ Bỏ qua      │ Process auto │
        └─────────────┴──────────────┘
```

| Score | Quadrant | Action |
|---|---|---|
| **15–25** | KILL ZONE | Mitigate **ngay tuần này**. Founder block 4-5h/tuần |
| **5–14** | Watch / Mitigate | Đưa vào roadmap, fix gradually |
| **1–4** | Accept | Quarterly review, bỏ qua hằng ngày |

---

### 2.8 Founder always-on-call playbook

#### Big company vs Startup reality

| **Big company playbook** | **Startup reality (5–10 người)** |
|---|---|
| Incident Commander rotation | Bạn **LÀ** Incident Commander |
| Sev1 → Wake CEO + Counsel | Bạn **LÀ** CEO. Bạn **LÀ** Counsel |
| Status page update | Twitter từ founder |
| PR team handle media | Bạn **LÀ** PR team |
| Postmortem báo cáo Board | Báo cáo Board = chính bạn |
| Sev tier escalation (1/2/3/4) | Chỉ có "crisis hay không" |

> **Implication:** Playbook startup phải đơn giản đến mức founder *mệt mỏi 3h sáng cũng làm theo được*.

---

### 2.9 30 phút đầu — 3 quyết định

> *In a viral crisis, hour 1 matters more than hour 24.*

Vì sao? Vì narrative formed trong giờ đầu. Sau đó — bạn defensive forever.

#### 3 quyết định cố định

```
0–5 phút:  VERIFY            (Đây có thật là AI của mình không?)
              ↓
5–15 phút: STOP THE BLEEDING (Tắt cái gì? 4 options)
              ↓
15–30 phút: COMMUNICATE       (Ai biết, theo thứ tự?)
```

#### Decision 1 — VERIFY (0–5 phút)

Câu hỏi: *Đây có thật là AI của mình không?*

**Action:**
- Check log Helicone hoặc LangFuse — **5 phút**
- Tìm timestamp + user ID + full conversation
- Verify vs photoshop, prank, fake screenshot

> Đây là tại sao **R2 (Rails) phải có log**. Không log = không verify được.

#### Decision 2 — STOP THE BLEEDING (5–15 phút)

Câu hỏi: *Tắt cái gì?* — 4 options:

| Option | Mô tả | Khi nào dùng |
|---|---|---|
| **Hard kill** | Tắt toàn bộ AI feature. Service down 100%. | Last resort. Khi viral đã quá tệ (DPD) |
| **Soft kill** | Switch sang rule-based fallback. Service vẫn chạy nhưng degraded. | Best option. Cần code fallback **trước** crisis |
| **Block 1 user** | Chỉ block user gây ra crisis. 99% user vẫn dùng. | Khi là user-specific issue |
| **Tighten prompt** | Add rule chặn behavior. Deploy ngay. | Nhanh nhất. Phù hợp với prompt injection |

> **Pro tip:** Code fallback rule-based chatbot **trong tuần đầu** sau khi launch AI feature. Test fallback quarterly. Khi crisis → flip 1 env var. Không code mới lúc panic.

#### Decision 3 — COMMUNICATE (15–30 phút)

Câu hỏi: *Ai cần biết, theo thứ tự?*

| # | Audience | Channel | Voice |
|---|---|---|---|
| 1 | **Customer affected** | DM cá nhân | Founder voice (xem template §2.10) |
| 2 | **Team** | Slack #all | "Có incident. I'm handling. Will update." |
| 3 | **Public** | 1 tweet ngắn | Founder voice, không corporate |
| 4 | **Investor** | Email update sau 24h | Sau khi đã contain |

---

### 2.10 Customer comm template

> **Pattern: Founder voice + Honest + Specific compensation + Direct contact.**

#### Template (English — adapt cho tiếng Việt nếu customer Việt)

```
Subject: From [Founder] re: what just happened

Hi [Customer],

This is [Founder] -- I personally saw the issue with our AI today.

What happened:    "Our chatbot told you policy is X. That's wrong."
What I'm doing:   "Disabled it. Reviewing logs personally."
Making it right:  "Refunding $650 today -- no forms."
Calling in 24h:   [Founder direct phone/Calendly]

-- [Founder name]
[founder@company personal email, NOT support@]
```

#### Phân tích từng dòng

| Dòng | Tại sao quan trọng |
|---|---|
| `Subject: From [Founder]` | Không "Customer Service". Founder name → personal |
| `This is [Founder]` | Personal voice từ đầu |
| `I personally saw` | Founder *tự* thấy. Không "our team noticed" |
| `What happened: 1 sentence` | Honest. Không spin. Không "deeply regret" |
| `What I'm doing` | Specific action với "I", không "we" |
| `Making it right: $650 -- no forms` | Specific $. Specific today. "No forms" — vì customer ghét forms |
| `Calling in 24h: [direct phone]` | Founder direct. Không "someone will reach out" |
| `founder@company` | Personal email. Không support@ |

#### Tiếng Việt version

```
Tiêu đề: Từ [Founder] về việc vừa xảy ra

Chào [Tên KH],

Đây là [Founder] -- em vừa thấy vấn đề với AI của bên em.

Việc xảy ra:        "Chatbot nói anh/chị policy X. Đó là sai."
Em đang làm gì:     "Đã disable. Em đang review log để check."
Em sửa thế nào:     "Refund 650K hôm nay -- không cần form."
Em gọi anh/chị 24h: [SĐT trực tiếp founder]

-- [Founder]
[founder@company]
```

> Big company không thể làm pattern này — vì legal block, PR rewrite, CEO không có thời gian. Startup founder *có thể* và *nên* làm. **Đây là superpower của startup.**

---

### 2.11 Soft kill > Hard kill

#### So sánh

| | **Hard kill** | **Soft kill** |
|---|---|---|
| **Mô tả** | Tắt toàn bộ AI feature | Switch sang rule-based fallback |
| **Service availability** | 100% down | 90% available (degraded) |
| **Customer experience** | "Service unavailable" | Vẫn dùng được, response template |
| **Recovery time** | Phải code lại + deploy | Flip 1 env var |
| **Khi nào dùng** | Last resort | Default |

#### Code fallback chatbot — instructions

**Khi launch AI feature** (Day 1):
- Notion TODO: "Build fallback chatbot in week 2"

**Tuần 2 sau launch:**
- Code rule-based version (template responses, FAQ, link to support)
- Deploy ở fallback URL
- Test với 5 conversations

**Quarterly:**
- War game test: flip env var → verify fallback works → flip back
- Update FAQ template based on common questions

**Khi crisis:**
- Flip env var → fallback active trong 30 giây
- Done. Service vẫn chạy.

---

### 2.12 5 R's của startup risks (Type taxonomy)

Mỗi risk register comprehensive cover **cả 5 R's**:

```
1. R - Vendor risk           (OpenAI, Anthropic, AWS đổi)
2. C - Customer-facing risk  (chatbot bịa policy)
3. F - Founder-bandwidth     (founder ốm, key person)
4. R - Regulatory risk       (EU AI Act, VN, GDPR)
5. R - Reputational risk     (viral incident)
```

#### Common blindspots với mỗi type

| Type | Founder thường skip | Vì sao |
|---|---|---|
| Vendor | Pricing change, ToS update | Founder assume "vendor stable" |
| Customer-facing | Chatbot edge cases | Đã test happy path, không test edge |
| Founder-bandwidth | Founder ốm 3 ngày | Không nghĩ tới single point of failure |
| Regulatory | EU AI Act, VN AI Law | Nghĩ "luật chưa apply với startup nhỏ" |
| Reputational | Prompt injection | Không nghĩ user sẽ malicious |

> **Quy tắc:** Risk Register phải có *ít nhất 1 risk mỗi type*. Nếu thiếu type nào — bạn có blindspot.

---

## 3. 4 Workshops — Hướng dẫn chi tiết

### 3.1 Workshop 1 — Build 3 R's (15 phút)

**Output:** `rules_rails_ritual.md` — 1 trang.

#### Quy trình

**Bước 1.** Chọn **1 risk lớn nhất** cho startup AI của bạn.

Ví dụ:
- Nhân viên CS dùng AI nói sai policy với khách (Air Canada style)
- Kỹ sư paste customer data vào ChatGPT public
- AI hallucinate giá sản phẩm
- Prompt injection viral

> **Pro tip:** Chọn 1 thôi — đừng tham. Workshop sẽ đi sâu vào 1 risk thay vì lướt qua nhiều.

**Bước 2 — RULES (3 phút):** Viết 4 dòng rule:

| Dòng | Yêu cầu | Pass ✅ | Fail ❌ |
|---|---|---|---|
| Cấm cụ thể | Vendor name + action | "KHÔNG paste customer chat vào ChatGPT public" | "Cấm dùng AI sai mục đích" |
| Allowed alternative | Vendor + cost | "DÙNG OpenAI Enterprise (đã setup, $25/user)" | "Dùng tool an toàn" |
| Hậu quả vi phạm | Concrete | "Founder talk 1-1 → let go" | "Bị kỷ luật theo quy chế" |
| Update mechanism | Notion link | "Update qua [Notion link]" | (không có) |

**Bước 3 — RAILS (5 phút):** Chọn **2 tool concrete** để chặn tự động risk này.

Yêu cầu:
- Tên vendor cụ thể
- Cost $/tháng
- Total stack < $500/tháng

**Bước 4 — RITUAL (5 phút):** Viết **1 ritual hàng tuần** liên quan risk này.

Bao gồm: 1 question founder sẽ hỏi customer hoặc team — specific, không generic.

**Bước 5 — Self-check (2 phút):** Trả lời 2 câu hỏi:
- Tổng cost RAILS dưới $500/tháng?
- RITUAL implement được trong 1 tuần?

Nếu "không" cho 1 trong 2 → quá enterprise. Simplify.

#### Pass/Fail signals

| Pass ✅ | Fail ❌ |
|---|---|
| RULES có vendor name + cost | RULES generic "tool an toàn" |
| RAILS dưới $500/tháng | RAILS > $1000/tháng (enterprise tools) |
| RITUAL có question cụ thể founder hỏi | RITUAL "review thường xuyên" mơ hồ |
| Implement được trong 1 tuần | Cần hire compliance officer |

---

### 3.2 Workshop 2 — Risk Register (15 phút)

**Output:** `risk_register.md` — 3 risks.

#### Quy trình

**Bước 1.** Mở:
- PRD Day 17 (sản phẩm là gì)
- Burn rate Day 18 (để tính tháng runway)

Identify **3 risks** từ 3 type khác nhau:

| Type | Yêu cầu |
|---|---|
| **1 Vendor risk** | OpenAI rate limit / pricing / ToS update — kiểu Replika |
| **1 Customer-facing AI risk** | Chatbot bịa policy — kiểu Air Canada |
| **1 Founder-bandwidth risk** | Founder ốm 3 ngày, critical bug không fix |

> **Pro tip:** Founder bandwidth risk thường skip nhất. Đừng skip — đây là single point of failure thật sự với startup 5-người.

**Bước 2.** Viết mỗi risk theo công thức:

```
If    [cause]
Then  [event]
Leading to  [tháng runway mất, KHÔNG phải $ hay %]
```

**Bước 3.** Chấm Likelihood (1-5), Impact (1-5 theo bảng):

| Runway lost | Impact score |
|---|---:|
| <1 tháng | 1 |
| 1–2 tháng | 2 |
| 3 tháng | 3 |
| 3–6 tháng | 4 |
| >6 tháng | 5 |

Tính Score = L × I.

**Bước 4.** Vẽ 2x2 matrix nhanh. Risk nào ở **KILL ZONE** (Score ≥ 15)?

KILL ZONE risk = priority cho Workshop 3 (Incident Playbook).

#### Quy đổi $ → tháng runway (cho startup của bạn)

Trước workshop, tính sẵn:

```
Burn rate của bạn: $___/tháng

→ $5,000 mất = ___ tháng runway
→ $50,000 mất = ___ tháng runway
→ $500,000 mất = ___ tháng runway
```

#### Pass/Fail signals

| Pass ✅ | Fail ❌ |
|---|---|
| Đo bằng tháng runway | Đo bằng $ hoặc % users |
| Có Founder-bandwidth risk | Skip founder risk |
| Vendor risk specific (rate limit / ToS / pricing) | "OpenAI có thể đổi" mơ hồ |
| Likelihood realistic | Tất cả Likelihood = 5 |
| Có ít nhất 1 risk ở KILL ZONE | Tất cả risks score thấp (overconfident) |

---

### 3.3 Workshop 3 — Incident Playbook (15 phút)

**Output:** `incident_playbook.md` — 1 trang.

#### Tình huống

```
9h30 sáng. Customer của bạn tweet screenshot:
AI của startup bạn vừa nói SAI 1 thông tin về sản phẩm cho khách.
200 retweets trong 30 phút. Đang có signal viral.
```

Đây là DPD scenario adapt cho startup nhỏ.

#### Quy trình

**Bước 1 — Verify (3 phút):**
- Bạn check log ở đâu? (cụ thể URL hoặc tool: Helicone? LangFuse? Database?)
- Cách verify nhanh đó là AI thật vs photoshop?

> **Pro tip:** Cụ thể URL/command. Không "sẽ check log" — phải biết check ở đâu.

**Bước 2 — Stop the bleeding (5 phút):**
- Chọn 1 trong 4 options: hard kill / soft kill / block 1 user / tighten prompt
- Giải thích lý do

**Bước 3 — Customer comm (5 phút):**
- Viết DM cụ thể cho customer affected, theo template §2.10
- Founder personal voice ("I", không "we")
- Specific compensation
- Direct contact (phone/Calendly)

**Bước 4 — Public response (2 phút):**
- 1 tweet ngắn từ founder
- Dưới 280 ký tự
- Không corporate statement

#### Template Public tweet

```
Hi everyone — I'm [Founder]. Just saw the chatbot issue.
We've disabled the AI element while we fix it.
More update in 24h. Reaching out to [@customer] directly now.
— [Founder]
```

(Dưới 280 ký tự. Personal. Action. Promise next update.)

#### Pass/Fail signals

| Pass ✅ | Fail ❌ |
|---|---|
| Verify cụ thể URL / endpoint | "Sẽ check log" |
| Stop bleeding chọn rõ + lý do | "Tùy tình huống" |
| Comm dùng "I" personal | Dùng "we" corporate |
| Compensation specific ($X today) | "Sẽ compensate phù hợp" |
| Public tweet < 280 ký tự | Tweet dài 500+ ký tự |
| Founder voice xuyên suốt | Sound như PR template |

---

### 3.4 Lab 4 — AI Vibe Coding (50 phút)

**Output:** `risk_register_v2.md` — 10+ risks comprehensive với mitigation plan.

#### 5 steps

**Step 1 — Chuẩn bị input (5 phút).**
- Mở PRD Day 17
- Mở Roadmap Day 20
- Mở Risk Register Workshop 2

**Step 2 — Run AI CRO Prompt (10 phút).**
- Copy prompt từ §4.1 dưới đây
- Paste prompt + paste tài liệu vào Claude/ChatGPT
- Run, đọc output
- Đánh dấu risk nào surprising

**Step 3 — Đối chiếu Workshop 2 (15 phút).**

4 câu hỏi:
| Câu hỏi | Output |
|---|---|
| Risk nào AI tìm ra mà bạn miss? | List ra |
| Risk nào bạn có mà AI miss? | Có thể context-specific. AI không biết. |
| Risk nào cả 2 đều có? | High confidence |
| Risk nào hai bên rate khác nhau? | Discuss |

**Step 4 — Update Risk Register (10 phút).**
- Merge 2 lists
- Loại bỏ duplicate
- Giữ top 10 risks ưu tiên cao nhất

**Step 5 — Generate mitigation (10 phút).**
- Cho mỗi risk top 5 (KILL ZONE), prompt AI generate 3 mitigation options
- Pick best

#### Quality gate (7 mục)

Risk Register v2 pass khi:

```
[ ] Có ≥ 10 risks (tăng từ 3 risks Workshop 2)
[ ] Cover cả 5 type (Vendor / Customer / Founder / Regulatory / Reputational)
[ ] Mỗi risk theo If-Then-Leading to với tháng runway
[ ] ≥ 2 risks bạn không nghĩ ra, AI tìm ra (chứng minh AI augmentation)
[ ] Top 5 KILL ZONE có mitigation founder-implementable trong 1 tuần
[ ] Mitigation cost < $500/tháng
[ ] Có ít nhất 1 regulatory risk (EU AI Act / VN / GDPR)
```

> Không pass đủ 7 mục → run prompt lại với context cụ thể hơn.

---

## 4. Prompts cho AI Vibe Coding (English-only)

> **Lưu ý:** Tất cả prompt giữ tiếng Anh 100% để AI giữ ngữ nghĩa ổn định. Thảo luận kết quả bằng tiếng Việt.

### 4.1 AI CRO Audit Prompt (main prompt cho Lab 4)

```
Act as a CRO for a Series Seed AI startup (5 people, 12mo runway). NOT Series B.

3 startup AI deaths to learn from:
- Air Canada-style: chatbot hallucinated policy → customer sued, $812 + precedent
- Replika-style: vendor change + silent comm → 75K users revolted, MRR -50%
- DPD-style: prompt injection → viral 1.7M views, brand damage

PRD + roadmap + burn rate:
[paste your PRD + Architecture + Roadmap + burn rate]

Identify TOP 10 RISKS specific to this startup. Format:

RISK N: [short name, 3-5 words]
- Type: [Vendor / Customer-facing / Founder-bandwidth / Regulatory / Reputational]
- If: [specific cause] / Then: [specific event]
- Leading to: [impact in MONTHS OF RUNWAY, not $ or % users]
- Likelihood (1-5): [score with reasoning]
- Impact (1-5 by runway): [1=<1mo, 5=>6mo]
- Mitigation: [3 actions, founder-implementable, <$500/month]

Constraints:
- BE SPECIFIC to this startup, not generic AI risks
- INCLUDE 2+ vendor risks (OpenAI rate limit, pricing, ToS)
- INCLUDE 1+ founder-bandwidth risk
- INCLUDE 1+ regulatory risk (EU AI Act, VN AI Law, GDPR)
- IGNORE PR-only Twitter drama
- FOCUS on financial survival risks

Be ruthless. Better hear from you than a real lawsuit.
```

> **Pro tip:** Run prompt này 2-3 lần với cùng input. Mỗi lần AI có output hơi khác. Merge cả 3 lần — coverage tốt hơn.

---

### 4.2 RULES Sanity Check (sau Workshop 1)

Dùng để kiểm tra RULES của bạn có actionable không.

```
Act as an AI safety advisor at a Series Seed AI startup.
You've seen 50+ startup policies — most are corporate cliché copies that nobody reads.

Below is my AI Safety Rules document:

[paste your rules_rails_ritual.md]

Critique it on 5 dimensions:

1. SPECIFICITY
   Quote any sentence that's generic ("don't misuse AI", "protect company data").
   Rewrite each as specific (vendor name + action).

2. ACTIONABILITY
   For each rule, can a new hire on Day 1 know what to do?
   If not, rewrite to be actionable.

3. ALTERNATIVE PATH
   For each "DON'T", is there a clear "DO" alternative with vendor + cost?
   If missing, suggest one.

4. CONSEQUENCE CLARITY
   Are violation consequences specific?
   "Will be disciplined" → bad. "Founder 1-1 talk → let go" → good.

5. STARTUP-FIT
   Is this lightweight enough for 5-person team?
   Or is it copied from a corporate template?

Score 1-10 with reasoning. Then provide rewritten version that fixes all issues.
```

---

### 4.3 RAILS Stack Optimizer

Dùng khi RAILS quá đắt hoặc thiếu coverage.

```
I'm a Seed AI startup founder with 5 engineers, $200K runway, 12 months left.

My current RAILS stack for AI safety:
[list your tools + costs]

Risks I'm trying to mitigate:
[list your top 5 risks from Workshop 2]

Audit my stack on 4 dimensions:

1. COVERAGE GAPS
   Which risks do I NOT have a tool for?
   Suggest tools (free or <$100/mo) to fill gaps.

2. OVERSPENDING
   Which tools are enterprise-grade overkill for my size?
   Suggest cheaper alternatives.

3. FREE TIER MAXIMIZATION
   Which tools have free tiers I'm not using?
   Suggest configs.

4. TOTAL BUDGET
   What's my total stack cost? Should be <$500/month for 5-person team.
   If over, suggest cuts.

Output: optimized stack with vendor names, costs, and setup priority order
(week 1 / week 2 / week 4).
```

---

### 4.4 RITUAL Generator

Dùng khi bí ý tưởng cho RITUAL.

```
I'm a Seed AI startup founder. My product is [describe in 1 sentence].
My biggest AI risk is [from Workshop 1].

Generate 5 weekly/monthly rituals tailored for THIS specific risk
that I (founder) can implement WITHOUT additional headcount.

For each ritual:
- Name (2-4 words)
- Duration (15min / 30min / 1h)
- Frequency (weekly / monthly / quarterly)
- Specific action steps
- 1 customer/team question I'll ask
- Expected output/insight

Constraints:
- Each ritual must be < 1 hour
- Total time commitment from founder: < 3 hours/week
- No software needed (use Notion/Slack/Phone)
- Must produce actionable insight (not just "feel good")

Be specific. "Friday review" is too vague — what exactly do I review?
```

---

### 4.5 Risk Register Critique

Dùng sau Workshop 2 để stress-test risk register.

```
Act as a senior risk analyst who has reviewed 100+ Seed startup risk registers.

Below is my risk register:

[paste your risk_register.md]

Critique on 6 dimensions:

1. SPECIFICITY
   Quote any risk that's generic ("AI may make mistakes").
   Rewrite as specific If-Then-Leading to.

2. RUNWAY MEASUREMENT
   Are impacts measured in MONTHS OF RUNWAY, not $ or %?
   Convert any non-runway measurements.

3. TYPE COVERAGE
   Do I have at least 1 risk of each type:
   Vendor / Customer-facing / Founder-bandwidth / Regulatory / Reputational?
   Identify missing types.

4. LIKELIHOOD CALIBRATION
   Are my Likelihood scores realistic, or am I being overconfident
   (too low) or paranoid (too high)?
   Suggest adjustments based on industry data.

5. KILL ZONE PRIORITIZATION
   For each risk in KILL ZONE (score >= 15):
   - Is the mitigation founder-implementable in 1 week?
   - Is the cost < $500/month?
   - Will it actually reduce L or I (not just track it)?

6. BLINDSPOTS
   What risks am I likely missing for my product type?
   Common blindspots:
   - Tokenizer/embedding vendor risk
   - Auth provider (Auth0, Clerk) downtime
   - Founder single point of failure
   - International data transfer (GDPR)
   List any I should add.

Be brutally honest. Score 1-10 with reasoning.
```

---

### 4.6 Incident Playbook Reviewer

Dùng sau Workshop 3 để verify playbook actionable.

```
Act as a reliability engineer who's run incident response at Stripe + 3 startups.

Below is my incident playbook:

[paste your incident_playbook.md]

Stress-test on 5 dimensions:

1. 3-AM TEST
   If I (founder) get paged at 3am after only 2 hours of sleep,
   can I follow this playbook step-by-step?
   Identify any step that requires creative thinking — those should be pre-decided.

2. VERIFY STEP
   Is the verify step specific?
   "Check logs" → bad. "Open Helicone, filter user_id, screenshot conversation" → good.

3. STOP-THE-BLEEDING SPECIFICITY
   Of the 4 options (hard/soft/block/tighten), is the criteria
   for choosing each option clear?

4. CUSTOMER COMM
   Does the comm use:
   - First person "I" (not "we")
   - Specific compensation (not "we'll make it right")
   - Direct contact (founder phone/Calendly, not support@)

5. TIME-BOXING
   Is each step time-boxed?
   "Verify in 5 min, decide in 10 min" → good.
   "Take time to investigate" → bad.

Be ruthless. Crisis is not the time to read 5 pages.
The playbook should fit on 1 page that founder can scan in 30 seconds.
```

---

## 5. Checkpoints — Output yêu cầu

### 5.1 Checkpoint 1 — RULES + RAILS + RITUAL (cuối Block 1, 10:00)

**Output:** `rules_rails_ritual.md` — 1 trang.

**Pass signals:**
- RULES có vendor name + cost cụ thể
- RAILS dưới $500/tháng total
- RITUAL có question founder cụ thể sẽ hỏi customer/team
- Implement được trong 1 tuần

**Fail signals:**
- Generic "tool an toàn"
- Stack > $1000/tháng (enterprise tools)
- Cần hire compliance officer
- RITUAL "review thường xuyên" mơ hồ

---

### 5.2 Checkpoint 2 — Risk Register (cuối Block 2, 10:45)

**Output:** `risk_register.md` — 3 risks.

**Pass signals:**
- 3 risks từ 3 type khác nhau (bao gồm Founder-bandwidth)
- Mỗi risk theo If-Then-Leading to
- Impact đo bằng tháng runway
- Có ít nhất 1 risk ở KILL ZONE

**Fail signals:**
- Skip founder bandwidth risk
- Đo bằng $ hoặc % users
- Vendor risk generic ("OpenAI có thể đổi")
- Tất cả Likelihood 5 hoặc tất cả 1

---

### 5.3 Checkpoint 3 — Incident Playbook (cuối Block 3, 11:45)

**Output:** `incident_playbook.md` — 1 trang.

**Pass signals:**
- Verify step cụ thể (URL Helicone)
- Stop-the-bleeding option chosen với lý do
- Customer comm dùng "I" personal
- Compensation specific ($X today)
- Public tweet < 280 ký tự

**Fail signals:**
- "Sẽ check log" mơ hồ
- "Tùy tình huống" không quyết định
- Comm dùng "we" corporate
- "Sẽ compensate phù hợp"
- Tweet > 280 ký tự

---

### 5.4 Checkpoint 4 — Risk Register v2 (cuối Lab 4, 12:35)

**Output:** `risk_register_v2.md` — 10+ risks comprehensive.

**Pass signals (7 mục):**
- ≥ 10 risks
- Cover cả 5 type
- If-Then-Leading to với tháng runway
- ≥ 2 risks AI tìm ra (bạn không nghĩ ra)
- Top 5 KILL ZONE có mitigation founder-implementable
- Mitigation cost < $500/tháng
- Có ít nhất 1 regulatory risk

**Fail signals:**
- < 10 risks
- Thiếu type (đặc biệt Founder-bandwidth, Regulatory)
- Mitigation generic "improve security"
- Mitigation > $1000/tháng (enterprise)

---

### 5.5 Final Checklist — Trước 13:00

```
[ ] 1. rules_rails_ritual.md  — 3 R's cho 1 risk lớn nhất
[ ] 2. risk_register.md       — 3 risks (Vendor/Customer/Founder-bandwidth)
[ ] 3. incident_playbook.md   — 1 trang founder always-on-call
[ ] 4. risk_register_v2.md    — 10+ risks AI-augmented + mitigation
[ ] 5. Tất cả files có vendor name cụ thể, cost cụ thể, runway cụ thể
[ ] 6. Nén ZIP: [Tên]_Day21.zip
[ ] 7. Nộp LMS trước 13:00
```

**Minimum bar:** Nếu một Series A VC mở 4 file của bạn lúc 9h sáng, họ sẽ:
- **Đọc hết** trong 5 phút?
- **Hiểu** governance approach + risk awareness của founder?
- **Trust founder** hơn 90% startup khác họ thấy?

Nếu trả lời CÓ cho cả 3 — package của bạn pass.

---

## 6. Rubric & Submission

### 6.1 Cách nộp bài

| Mục | Yêu cầu |
|---|---|
| **Nộp khi nào** | Cuối buổi sáng Day 21 — **trước 13:00** |
| **Nộp ở đâu** | Submit trực tiếp trên LMS |
| **Tên file** | `[Tên]_Day21.zip` |
| **Bao gồm** | 4 files trong 1 thư mục |

> **KHÔNG có BTVN.** Day 21 hoàn tất trong buổi sáng. Đây là ngày đầu Chương 5.

---

### 6.2 Rubric — 100 điểm, 5 tiêu chí

| # | Tiêu chí | Điểm |
|---|---|---:|
| 1 | **3 R's lightweight** (Rules/Rails/Ritual phù hợp seed-stage) | 20 |
| 2 | **Risk Register theo runway** | 20 |
| 3 | **Incident Playbook actionable** | 20 |
| 4 | **AI Augmentation evidence** (Lab 4) | 20 |
| 5 | **Founder voice xuyên suốt** | 20 |

---

#### Tiêu chí 1 — 3 R's lightweight (20 điểm)

- ✓ RULES có vendor name + cost cụ thể
- ✓ RAILS total < $500/tháng
- ✓ RITUAL có question cụ thể founder hỏi
- ✓ Implement được trong 1 tuần
- ✓ Founder-led, không cần hire compliance

**Điểm cao nhất:** RULES dưới 1 trang nhưng cover 4 câu hỏi (cấm gì / được gì / hậu quả / update); RAILS có ít nhất 1 free tool; RITUAL có "Customer Friday" với question cụ thể.

---

#### Tiêu chí 2 — Risk Register theo runway (20 điểm)

- ✓ 3 risks từ 3 type khác nhau (bao gồm Founder-bandwidth)
- ✓ If-Then-Leading to chuẩn
- ✓ Impact đo bằng tháng runway, không $ hay %
- ✓ Likelihood realistic (không tất cả 5)
- ✓ Có ít nhất 1 risk ở KILL ZONE

**Điểm cao nhất:** 3 risks specific với vendor name, có 1 founder-bandwidth risk thật sự (không skip), tháng runway tính chính xác từ burn rate.

---

#### Tiêu chí 3 — Incident Playbook actionable (20 điểm)

- ✓ Verify step cụ thể (URL/tool name)
- ✓ Stop-the-bleeding chosen với lý do rõ
- ✓ Customer comm dùng "I" personal voice
- ✓ Compensation specific ($X today, no forms)
- ✓ Pass 3-AM test (founder mệt mỏi cũng làm theo được)

**Điểm cao nhất:** Playbook 1 trang founder có thể scan 30 giây; comm template dùng được ngay không edit.

---

#### Tiêu chí 4 — AI Augmentation evidence (20 điểm)

- ✓ ≥ 10 risks (tăng từ 3 manual)
- ✓ Cover cả 5 type
- ✓ ≥ 2 risks bạn ghi nhận "AI tìm ra mà tôi miss"
- ✓ Top 5 KILL ZONE có 3 mitigation options mỗi risk
- ✓ Mitigation < $500/tháng

**Điểm cao nhất:** Có comment tự reflection cho từng AI-found risk: "Tôi miss vì tôi assume X, nhưng thực ra Y" — chứng tỏ học từ AI.

---

#### Tiêu chí 5 — Founder voice xuyên suốt (20 điểm)

- ✓ RULES viết bằng founder voice
- ✓ Customer comm template dùng "I", không "we"
- ✓ Public tweet personal, không corporate
- ✓ Mitigation actions có "I will", không "we should"
- ✓ Toàn bộ package đọc như founder talk to founder

**Điểm cao nhất:** Toàn bộ 4 files có consistent voice. Đọc như diary của founder, không như corporate document.

---

### 6.3 Grade bands

| Band | Điểm | Ý nghĩa |
|---|---:|---|
| Outstanding | 90–100 | Có thể show VC ngay tuần sau, không cần edit |
| Strong | 75–89 | Cần 1 round refine với mentor |
| Pass | 60–74 | Hiểu framework, package còn enterprise-y |
| Needs rework | 40–59 | Sai concept core (đo $ thay tháng runway, dùng "we" thay "I") |
| Fail | <40 | Chưa đạt minimum bar |

---

### 6.4 Lưu ý khi làm bài

- **Đừng dùng enterprise tools** (Symantec, Zscaler) trong RAILS — mất điểm Tiêu chí 1
- **Đừng đo bằng $** — phải convert sang tháng runway
- **Đừng skip Founder-bandwidth risk** — đây là blindspot lớn nhất của founder
- **Đừng dùng "we" trong customer comm** — phải "I" personal
- **Đừng skip Step 5 mitigation** trong Lab 4 — đó là output cuối
- **Đừng paste 1 trang PRD** vào AI prompt — paste full PRD để AI có context
- **Đừng accept AI output blindly** — đối chiếu với context startup của bạn

---

## 7. References

### Core readings (case studies)

1. **Moffatt v. Air Canada, 2024 BCCRT 149**
   https://www.canlii.org/en/bc/bccrt/doc/2024/2024bccrt149/
   Phán quyết landmark. Đọc paragraphs 27-28 cho Tribunal Member Rivers's reasoning.

2. **BC Tribunal Confirms Companies Remain Liable for AI Chatbot — ABA**
   https://www.americanbar.org/groups/business_law/resources/business-law-today/2024-february/bc-tribunal-confirms-companies-remain-liable-information-provided-ai-chatbot/
   Phân tích legal implications cho mọi business dùng chatbot.

3. **Replika ERP removal & Reddit discourse — Sage Journals**
   https://journals.sagepub.com/doi/10.1177/23780231241259627
   Academic analysis of r/Replika 75K user revolt.

4. **DPD chatbot incident — TIME**
   https://time.com/6564726/ai-chatbot-dpd-curses-criticizes-company/
   1.7M views, 24h response, brand damage analysis.

### Frameworks & best practices

5. **OpenAI Enterprise Privacy & Security**
   https://openai.com/enterprise-privacy
   Hiểu data not used for training, SOC 2, SSO.

6. **Anthropic — Claude for Work**
   https://www.anthropic.com/claude/team
   Enterprise tier alternative.

7. **NextDNS — DNS-based filtering**
   https://nextdns.io/
   $40/mo cheap firewall startup.

8. **Helicone — LLM observability**
   https://helicone.ai/
   Free tier 100K req/mo, log mọi LLM call.

9. **git-secrets — AWS Labs**
   https://github.com/awslabs/git-secrets
   Free OSS, chặn secrets vào git.

### Further reading (optional)

10. **Black Swan — Nassim Taleb**
    Foundational cho risk thinking — fat-tail events, không phải Gaussian.

11. **Antifragile — Nassim Taleb**
    Khái niệm "antifragile" — design system gain từ disorder.

12. **The Field Guide to Understanding Human Error — Sidney Dekker**
    Incident analysis without blame culture.

13. **EU AI Act**
    https://artificialintelligenceact.eu/
    Read Article 50+ về transparency obligations cho chatbot.

### Quick reference — câu chốt Day 21

| Câu chốt |
|---|
| "Big company governance = avoid lawsuit. Startup governance = avoid death." |
| "Phanh Brembo không sinh ra để bạn đi chậm. Sinh ra để bạn DÁM chạy 300 km/h." |
| "Chatbot của bạn = legally binding spokesperson từ ngày 1." |
| "Rules là giấy. Rails là code. Ritual là behavior." |
| "Không tool nào replace được founder hỏi customer thật." |
| "Đo risk theo tháng runway — không theo $ hay Twitter mentions." |
| "Vendor risk + Communication risk = 2 killers lớn nhất." |
| "Bạn LÀ pager. Bạn LÀ IC. Bạn LÀ Counsel." |
| "In a viral crisis, hour 1 matters more than hour 24." |
| "Founder voice + Honest + Specific compensation + Direct contact = trust signal." |
| "Code fallback chatbot trong tuần đầu sau launch." |
| "Better hear it from your AI than from a real lawsuit." |
| "From speed → to safety → to scale." |

---

*Lái nhanh — với phanh tốt. From speed → to safety → to scale.*
