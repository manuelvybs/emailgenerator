# vybs-benchmarks.md
# VYBS — Email Performance Benchmarks & Tracking

This file defines performance standards for VYBS email campaigns in Braze.
Use it to evaluate campaigns, flag underperformers, and identify A/B test priorities.
Update the "VYBS Actuals" columns as you pull real data from Braze.

---

## 1. PRIMARY BENCHMARKS — GAMING & REWARDS VERTICAL (2025)

These are your target ranges. VYBS sits at the intersection of Gaming + Rewards/Loyalty apps.

| Metric | Below Average | Average | Good | Excellent | Source |
|---|---|---|---|---|---|
| Unique Open Rate | <20% | 20–28% | 28–35% | 35%+ | Omnisend/Braze 2025 |
| Click-Through Rate (CTR) | <1.5% | 1.5–3% | 3–5% | 5%+ | MailerLite/Braze 2025 |
| Click-to-Open Rate (CTOR) | <8% | 8–12% | 12–20% | 20%+ | HubSpot/Braze 2025 |
| Unsubscribe Rate | >1% | 0.5–1% | 0.2–0.5% | <0.2% | Brevo 2025 |
| Hard Bounce Rate | >3% | 1–3% | 0.5–1% | <0.5% | Braze guidelines |
| Soft Bounce Rate | >5% | 2–5% | 1–2% | <1% | Braze guidelines |
| Spam Complaint Rate | >0.1% | 0.08–0.1% | 0.03–0.08% | <0.03% | Google/Braze 2025 |
| Click-to-Conversion Rate | <5% | 5–11% | 11–15% | 15%+ | Omnisend games 2025 |

### Key gaming stats (2025 industry data)
- The games industry click-to-conversion rate reached 17.61% in 2025, up from 11.6% in 2023 — this is your conversion benchmark
- Automated emails accounted for just 2% of sends but drove 30% of revenue, earning 16x more per send than scheduled campaigns — prioritize Canvas automations
- Braze recommends pairing open rate with click-through and conversion data given Apple MPP inflation

### Apple MPP warning
Open rates are inflated for Apple Mail users (~46% of all email clients). Apple pre-fetches the tracking pixel even if the user never opens.
- **Never make decisions based on open rate alone**
- **Primary signals to trust: CTR, CTOR, conversions, revenue per email**
- In Braze, use "Estimated Human Unique Opens" (machine-open-filtered metric) when available

---

## 2. VYBS ACTUALS — CAMPAIGN PERFORMANCE TRACKER

Update this table after each campaign. Pull from Braze Campaign Analytics.

### Campaigns

| Campaign Name | Date | Segment | Sends | Open % | CTR % | CTOR % | Unsub % | Bounce % | Conversions | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| *(add your data here)* | | | | | | | | | | |
| | | | | | | | | | | |
| | | | | | | | | | | |

### Canvas Performance

| Canvas Name | Date | Trigger | Entry Users | Completion % | CTR % | Revenue | Notes |
|---|---|---|---|---|---|---|---|
| *(add your data here)* | | | | | | | |
| | | | | | | | |

---

## 3. BENCHMARKS BY CAMPAIGN TYPE

Different email types have different expectations. Use these ranges per campaign category.

### Transactional / Triggered
*(reward confirmed, account created, purchase receipt)*
```
Open Rate:    45–60%    ← highest of all types, high intent
CTR:          8–15%
CTOR:         20–30%
Unsub:        <0.1%
Goal:         Confirmation + upsell to next action
```

### Onboarding / Welcome Series
*(day 0–7 new user flow)*
```
Open Rate:    35–55%    ← first email always highest
CTR:          5–10%
CTOR:         15–25%
Unsub:        <0.3%
Goal:         First earn / first redemption
```

### Lifecycle / Re-engagement
*(inactive 7d, 14d, 30d users)*
```
Open Rate:    15–25%    ← lower, disengaged audience
CTR:          2–5%
CTOR:         10–18%
Unsub:        <0.8%     ← expect higher, list hygiene benefit
Goal:         Return to app + any game session
```

### Promotional / Campaign
*(weekly digest, limited-time promos, gift card drops)*
```
Open Rate:    20–32%
CTR:          2–6%
CTOR:         10–20%
Unsub:        <0.5%
Goal:         Click to app / claim reward
```

### Win-back
*(inactive 30d+)*
```
Open Rate:    10–20%
CTR:          1–4%
CTOR:         8–15%
Unsub:        <2%       ← acceptable, cleaning list
Goal:         Any re-engagement signal
```

---

## 4. SUBJECT LINE BENCHMARKS

Based on 2025 industry data for gaming/consumer apps:

| Subject Line Type | Avg Open Rate Lift | Notes |
|---|---|---|
| Personalized (`{{first_name}}`) | +10–15% | Use on all campaigns |
| Emoji in subject | +5–10% (gaming) | Use 1 max, test carefully |
| Number/specific value | +8–12% | "You have 500 points" |
| Question format | +5–8% | "Ready to earn?" |
| Urgency (genuine) | +6–10% | Deadline must be real |
| Hype/spam language | −15–30% | "FREE!!!" → spam filter |
| ALL CAPS | −10–20% | Never use |
| 40–60 characters | Best length | Optimal for mobile |
| 6–10 words | Highest open rate | per multiple sources |

### Subject line formulas that work for VYBS
```
Reward/earn:    "{{first_name}}, your [X] points are waiting"
Urgency:        "24 hours left to claim your gift card"
New game:       "New game just dropped — start earning today"
Re-engagement:  "We saved your spot, {{first_name}}"
Weekly digest:  "This week on VYBS: earn more, play more"
Milestone:      "You're [X] points away from a $[Y] gift card"
```

---

## 5. SEND TIME BENCHMARKS

Based on gaming/consumer app data. All times local to user timezone.

| Day | Performance | Notes |
|---|---|---|
| Tuesday | ⭐⭐⭐ Best | Highest open + CTR across most verticals |
| Wednesday | ⭐⭐⭐ Best | Strong runner-up |
| Thursday | ⭐⭐ Good | Solid mid-week |
| Monday | ⭐⭐ Good | Good for re-engagement |
| Sunday | ⭐ Low | Gaming audience active but email-checking low |
| Friday | ⭐ Low | Weekend mindset, lower engagement |
| Saturday | ⭐ Lowest | Avoid for promotional sends |

| Time | Performance | Notes |
|---|---|---|
| 10–11am | ⭐⭐⭐ Best | Post-morning routine, inbox check |
| 6–8pm | ⭐⭐⭐ Best | Gaming primetime, post-work |
| 8–9am | ⭐⭐ Good | Morning inbox check |
| 12–1pm | ⭐⭐ Good | Lunch break |
| 4–5pm | ⭐ Low | Pre-commute distraction |

**VYBS recommendation:** Tuesday or Wednesday, 10am or 7pm local. Use Braze Intelligent Timing for at-scale sends.

---

## 6. DELIVERABILITY HEALTH THRESHOLDS

These are hard limits. If crossed, stop sending and investigate immediately.

| Signal | Safe | Investigate | STOP SENDING |
|---|---|---|---|
| Spam complaint rate | <0.03% | 0.03–0.08% | >0.08% |
| Hard bounce rate | <0.5% | 0.5–2% | >2% |
| Unsubscribe rate | <0.3% | 0.3–0.8% | >1% |
| Soft bounce rate | <2% | 2–5% | >5% |

### 2025 updated thresholds (Google + Microsoft)
Google now flags senders exceeding 0.3% spam complaint rate and recommends under 0.1% as best practice. Microsoft followed with similar policies in May 2025. High-complaint promotional sends now damage deliverability for transactional emails too.

**Action plan if you hit a threshold:**
1. Pause the campaign immediately
2. Check segment — are you mailing unengaged users?
3. Check suppression lists — did unsubscribers get added back?
4. Check email content — any spam trigger words?
5. Check send frequency — did you increase cadence recently?

---

## 7. ROI & REVENUE BENCHMARKS

| Metric | Industry Average | Gaming/Rewards | VYBS Target |
|---|---|---|---|
| Revenue per email sent | $0.18 (campaigns) | $0.30–$0.75 | *(track in Braze)* |
| Revenue per automated email | $2.87 | $3–$8 | *(track in Braze)* |
| Email marketing ROI | $36–42 per $1 spent | $40–76 per $1 | *(calculate quarterly)* |

Automated emails generated $2.87 per email sent on average, compared to $0.18 for standard campaign sends in 2025. This is why Canvas automations are your highest-leverage channel.

---

## 8. A/B TEST PRIORITY MATRIX

What to test first, ranked by expected impact for VYBS.

| Priority | Test | Hypothesis | Metric to watch |
|---|---|---|---|
| 1 | Subject line personalization | `{{first_name}}` vs generic | Open rate |
| 2 | Send time (10am vs 7pm) | Gaming users more active evenings | CTR |
| 3 | CTA button color (Gold vs Blue) | Gold = reward signal | CTR |
| 4 | Single CTA vs two CTAs | Focus drives more clicks | CTOR |
| 5 | Reward points shown vs hidden | Showing points = more urgency | Conversion |
| 6 | Short subject (5 words) vs long (10 words) | Curiosity gap | Open rate |
| 7 | Emoji in subject vs no emoji | Gaming audience tolerates emoji | Open rate |
| 8 | Dark bg email vs light bg email | VYBS dark theme vs clean | CTR |

---

## 9. METRICS GLOSSARY (BRAZE-SPECIFIC)

| Term | Definition | Braze location |
|---|---|---|
| Unique Opens | First open per user, deduped | Campaign Analytics |
| Machine Opens (MPP) | Apple Mail auto-prefetch — not real | Campaign Analytics |
| Estimated Human Unique Opens | Braze model removing machine opens | Campaign Analytics |
| Other Opens | Opens not labeled machine (likely real) | Campaign Analytics |
| Unique Clicks | First click per user per link | Campaign Analytics |
| Total Clicks | All clicks, including repeat | Campaign Analytics |
| CTR | Unique clicks / delivered | Campaign Analytics |
| CTOR | Unique clicks / unique opens | Campaign Analytics |
| Hard Bounce | Permanent delivery failure | Campaign Analytics |
| Soft Bounce | Temporary delivery failure (Braze retries) | Campaign Analytics |
| Deferral | Retry period delivery — Currents/Snowflake only | Currents |
| Spam Report | User marked as spam | Campaign Analytics |
| Revenue | Attributed purchase value (if Braze purchase events set up) | Campaign Analytics |
| Conversion Rate | Users who completed conversion event / delivered | Campaign Analytics |
| dispatch_id | Unique ID per send — use for Currents cross-referencing | Currents |

---

## 10. QUICK ANALYSIS PROMPTS FOR CLAUDE

When pasting Braze campaign data, use these prompts:

```
"Here is my Braze campaign data [paste data].
Compare against benchmarks in vybs-benchmarks.md.
Flag anything outside healthy ranges.
Identify the top 3 opportunities to improve."

"Here are my last 10 campaign results [paste data].
What patterns do you see in subject lines vs open rates?
What A/B tests should I run next?"

"My re-engagement Canvas has [X%] CTR. 
Based on benchmarks in vybs-benchmarks.md, is this good?
What changes to the flow or copy would improve it?"
```

---

*Sources: Omnisend 2025, Braze Resources 2025, MailerLite 2025, HubSpot 2025, Brevo 2025*
*Last updated: March 2026 | Update VYBS Actuals section monthly after Braze export*
