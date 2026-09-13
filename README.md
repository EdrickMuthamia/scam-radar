# Scam Radar

A cybersecurity tool that analyzes digital communications and returns a structured risk assessment to help users identify potentially fraudulent messages.

**Current stage:** Day 1 — Threat modeling and architecture design. No application code has been written yet.

---

## The Problem

Scam messages are one of the most common vectors for financial fraud in Kenya and across Africa. Victims receive fraudulent SMS messages, WhatsApp texts, and emails impersonating banks, mobile money services, government agencies, employers, and prize promotions. Many victims lose money because the messages look convincing and create a sense of urgency that bypasses critical thinking.

Existing solutions are either:
- Too generic (spam filters that miss context-specific scams)
- Too opaque (black-box AI with no explanation)
- Not localized (built for Western markets, miss M-Pesa and local patterns)

Scam Radar is designed to be explainable, locally aware, and honest about its confidence level.

---

## What Scam Radar Does

Scam Radar analyzes a submitted message and returns:

- A **risk score** from 0 to 100
- A **risk level**: LOW / SUSPICIOUS / HIGH / CRITICAL
- A **suspected scam category**
- A list of **detected indicators** that contributed to the score
- A plain-language **explanation**
- A **recommended action** for the user

### Example

**Input:**
```
Congratulations! You have won KSh 50,000. Click this link immediately to claim your prize.
```

**Output:**
```
Risk Score:    88 / 100
Risk Level:    CRITICAL
Category:      PRIZE_SCAM

Indicators:
  - Unexpected reward
  - Urgency language
  - Financial incentive
  - Request to click link
  - No sender verification

Explanation:
  This message contains multiple patterns commonly associated with prize scams,
  including an unsolicited reward, urgency pressure, and a link to claim funds.

Recommendation:
  Do not click the link. If you believe this may be legitimate, verify directly
  through the organization's official website or customer service number.
```

---

## What Scam Radar Does NOT Claim

Scam Radar does **not** say "this is definitely a scam" or "this sender is a criminal."

It says: **"This message contains patterns commonly associated with fraud. Exercise caution."**

This distinction matters because:
- No automated system achieves 100% accuracy
- Legitimate messages can contain suspicious-looking language
- Making false accusations creates legal and trust problems

---

## MVP Scope

The first version analyzes:
- SMS text
- WhatsApp-style text messages
- Email body text (plain text)

It does **not** yet analyze:
- Images or screenshots
- Attachments
- Voice messages
- Live URLs (link following)

---

## Scam Categories (Initial)

| Category | Description |
|---|---|
| FINANCIAL_SCAM | Generic financial fraud, payment requests, fake fees |
| JOB_SCAM | Fake job offers, upfront payment for employment |
| PRIZE_SCAM | Fake lottery, competition, or giveaway winnings |
| BANK_IMPERSONATION | Messages pretending to be from a bank |
| MOBILE_MONEY_SCAM | M-Pesa and mobile money fraud |
| PHISHING | Credential harvesting via fake login pages |
| SCHOLARSHIP_SCAM | Fake scholarship or bursary offers |
| ROMANCE_SCAM | Emotional manipulation leading to financial requests |
| ACCOUNT_TAKEOVER | OTP theft, password reset abuse |
| INVESTMENT_SCAM | Fake investment opportunities, Ponzi schemes |

---

## Risk Levels

| Score | Level | Meaning |
|---|---|---|
| 0–24 | LOW | No significant indicators detected |
| 25–49 | SUSPICIOUS | Some indicators present; verify before acting |
| 50–74 | HIGH | Multiple indicators; strong caution advised |
| 75–100 | CRITICAL | High-confidence fraud pattern detected |

---

## Target Users

**Phase 1 (MVP):**
- Individual consumers in Kenya who receive suspicious messages
- People who want a second opinion before clicking a link or sending money

**Phase 2 (API):**
- Banks and SACCOs wanting to warn customers
- Mobile money platforms
- Businesses wanting to protect employees
- Developers building consumer protection tools

---

## Technology Direction

We are starting simple and deliberately:

1. **Rule-based risk engine** — weighted indicators, explainable scores, no black-box AI
2. **Structured dataset** — labeled examples with categories, indicators, and expected scores
3. **REST API** — clean interface for future integrations
4. **No unnecessary complexity** — no microservices, no ML on Day 1

We will evaluate machine learning and LLM integration only after the rule-based engine is validated and a quality dataset exists.

---

## Project Structure

```
scam-radar/
├── docs/
│   ├── THREAT_MODEL.md       # Threat model, abuse scenarios, security controls
│   └── SCAM_CATEGORIES.md    # Detailed category definitions
├── data/
│   └── dataset_schema.md     # Dataset field definitions and structure
├── README.md
└── DAY1_REPORT.md            # Architecture decisions and Day 1 summary
```

---

## Development Roadmap

| Day | Focus |
|---|---|
| Day 1 | Threat model, scam categories, indicator taxonomy, scoring design, dataset schema |
| Day 2 | Initial labeled dataset (CSV), rule-based scoring engine implementation |
| Day 3 | REST API, input validation, basic rate limiting |
| Day 4 | Testing, false-positive tuning, edge cases |
| Day 5+ | Frontend, user reporting, whitelist management |

---

## Ethical Commitments

- We do not store user messages without explicit consent
- We do not claim certainty we do not have
- We do not hard-code accusations against specific individuals or companies
- We label all outputs as risk assessments, not verdicts
- We will publish our indicator taxonomy so users understand how scoring works

---

## Status

> Day 1 complete. Threat model and architecture defined. No application code written yet.
