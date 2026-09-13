# Scam Radar — Dataset Schema

**Version:** 0.1 (Day 1)

This document defines the structure of the labeled dataset that will be used to develop, test, and validate the risk-scoring engine.

---

## Guiding Principles

- We do NOT collect private user messages without explicit consent
- We do NOT create fake claims about real companies or real people
- All synthetic examples are clearly labeled as synthetic
- The dataset is a tool for building and testing detection logic, not a public accusation list

---

## CSV Schema

```
id, message, category, risk_level, indicators, source_type, language, country_context, expected_score, notes
```

---

## Field Definitions

### `id`
- Type: string
- Format: `SR-0001`, `SR-0002`, etc.
- Purpose: Unique identifier for each record. Used for referencing specific examples in tests and reports.

---

### `message`
- Type: string
- Purpose: The raw text of the message being analyzed.
- Rules:
  - No real personal names, phone numbers, or account numbers
  - Use placeholders: `[NAME]`, `[PHONE]`, `[ACCOUNT]`, `[AMOUNT]`
  - For synthetic examples, clearly construct the message to illustrate the category
  - For public examples, paraphrase to remove identifying information

---

### `category`
- Type: enum
- Allowed values:
  - `FINANCIAL_SCAM`
  - `JOB_SCAM`
  - `PRIZE_SCAM`
  - `BANK_IMPERSONATION`
  - `MOBILE_MONEY_SCAM`
  - `PHISHING`
  - `SCHOLARSHIP_SCAM`
  - `ROMANCE_SCAM`
  - `ACCOUNT_TAKEOVER`
  - `INVESTMENT_SCAM`
  - `LEGITIMATE` (for negative examples — messages that should NOT be flagged)
  - `UNKNOWN` (for ambiguous cases under review)
- Purpose: The ground-truth label for supervised evaluation.

---

### `risk_level`
- Type: enum
- Allowed values: `LOW`, `SUSPICIOUS`, `HIGH`, `CRITICAL`
- Purpose: The expected risk level output for this message.
- Mapping:
  - `LOW` → expected_score 0–24
  - `SUSPICIOUS` → expected_score 25–49
  - `HIGH` → expected_score 50–74
  - `CRITICAL` → expected_score 75–100

---

### `indicators`
- Type: pipe-separated string
- Format: `URGENCY|PAYMENT_REQUEST|IMPERSONATION`
- Purpose: The list of indicators that a human reviewer identified in this message.
- These are the ground-truth indicators used to validate that the scoring engine detects the right signals.
- See `INDICATOR_TAXONOMY.md` for the full list of valid indicator codes.

---

### `source_type`
- Type: enum
- Allowed values:
  - `synthetic` — message was constructed by the team to illustrate a pattern; never happened in reality
  - `public_example` — message pattern is based on publicly reported scam examples (paraphrased, no real PII)
  - `user_report` — message was submitted by a user who received it (requires consent; not used in Day 1)
- Purpose: Tracks data provenance so we know how much of the dataset is real vs. constructed.

---

### `language`
- Type: string (ISO 639-1 code)
- Examples: `en`, `sw`, `en-sw` (mixed English/Swahili)
- Purpose: Enables language-specific analysis and helps identify gaps in multilingual coverage.

---

### `country_context`
- Type: string (ISO 3166-1 alpha-2 country code)
- Examples: `KE` (Kenya), `NG` (Nigeria), `ZA` (South Africa), `GLOBAL`
- Purpose: Allows country-specific indicator sets and scoring adjustments without hard-coding Kenya into the core engine.

---

### `expected_score`
- Type: integer (0–100)
- Purpose: The score a human reviewer believes the engine should produce for this message.
- Used for: regression testing — if the engine's score deviates significantly from expected_score, the rule weights need review.
- Note: This is a target range, not an exact number. A tolerance of ±10 points is acceptable for initial testing.

---

### `notes`
- Type: string (optional)
- Purpose: Free-text field for reviewer comments, edge case explanations, or flagging ambiguous examples.
- Examples:
  - "This is a false-positive test case — legitimate bank message"
  - "Mixed language; Swahili urgency phrase in otherwise English message"
  - "Borderline case — could be FINANCIAL_SCAM or MOBILE_MONEY_SCAM"

---

## Example Records

```csv
id,message,category,risk_level,indicators,source_type,language,country_context,expected_score,notes
SR-0001,"Congratulations! You have won KSh 50,000. Click this link immediately to claim your prize: http://bit.ly/claim-now",PRIZE_SCAM,CRITICAL,URGENCY|UNEXPECTED_REWARD|FINANCIAL_INCENTIVE|SUSPICIOUS_URL|URL_SHORTENER,synthetic,en,KE,88,Classic prize scam with URL shortener
SR-0002,"Your M-PESA account has been suspended. Verify your PIN at http://safaricom-verify.net to restore access.",MOBILE_MONEY_SCAM,CRITICAL,IMPERSONATION|CREDENTIAL_REQUEST|SUSPICIOUS_URL|URGENCY|ACCOUNT_THREAT,synthetic,en,KE,92,M-Pesa impersonation with fake domain
SR-0003,"Dear [NAME], your application for the government bursary has been received. Pay KSh 500 processing fee to 0712XXXXXX to proceed.",SCHOLARSHIP_SCAM,HIGH,PAYMENT_REQUEST|FAKE_AUTHORITY|UNEXPECTED_OPPORTUNITY,synthetic,en,KE,65,Scholarship scam with upfront fee
SR-0004,"URGENT: Your KCB account shows suspicious activity. Call 0800-XXXXXX immediately or your account will be frozen.",BANK_IMPERSONATION,HIGH,URGENCY|IMPERSONATION|ACCOUNT_THREAT|FAKE_AUTHORITY,synthetic,en,KE,70,Bank impersonation without link — phone-based
SR-0005,"Hi [NAME], your order #45231 has been dispatched and will arrive tomorrow. Track here: https://dhl.com/track/45231",LEGITIMATE,LOW,,synthetic,en,KE,5,Legitimate delivery notification — should not be flagged
SR-0006,"Invest KSh 5,000 today and receive KSh 15,000 in 3 days. Guaranteed returns. WhatsApp [PHONE] to join.",INVESTMENT_SCAM,CRITICAL,UNREALISTIC_RETURN|GUARANTEED_PROFIT|PAYMENT_REQUEST|URGENCY,synthetic,en,KE,85,Investment scam with guaranteed return claim
SR-0007,"Pongezi! Umeshinda KSh 10,000 katika mchezo wetu. Piga simu [PHONE] sasa kudai zawadi yako.",PRIZE_SCAM,CRITICAL,URGENCY|UNEXPECTED_REWARD|FINANCIAL_INCENTIVE,synthetic,sw,KE,80,Swahili prize scam
SR-0008,"Your account password will expire in 24 hours. Click here to update: http://g00gle-accounts.com/reset",PHISHING,CRITICAL,URGENCY|CREDENTIAL_REQUEST|SUSPICIOUS_URL|IMPERSONATION|MISSPELLED_DOMAIN,synthetic,en,GLOBAL,90,Phishing with misspelled domain
SR-0009,"We are hiring 50 people for data entry work from home. Earn KSh 3,000 daily. No experience needed. Pay KSh 800 registration. Call [PHONE].",JOB_SCAM,HIGH,UPFRONT_PAYMENT|UNREALISTIC_SALARY|UNSOLICITED_OFFER,synthetic,en,KE,72,Job scam with registration fee
SR-0010,"Dear customer, your Equity Bank statement for March is ready. Log in at https://equitybank.co.ke to view.",LEGITIMATE,LOW,,synthetic,en,KE,8,Legitimate bank notification on official domain
```

---

## Dataset Size Targets

| Phase | Target Records | Composition |
|---|---|---|
| Day 2 (initial) | 50–100 | 80% scam examples, 20% legitimate (false-positive tests) |
| Week 2 | 300–500 | Balanced across all 10 categories + legitimate |
| Month 2 | 1,000+ | Include multilingual, edge cases, evasion examples |

---

## Data Quality Rules

1. Every record must have a valid `category`, `risk_level`, and `expected_score`
2. `indicators` must only contain codes from the approved indicator taxonomy
3. `source_type` must be accurate — never label synthetic data as `user_report`
4. No real personal information in any field
5. Ambiguous records go to `UNKNOWN` category until reviewed by a second person
6. The dataset must include at least 15% `LEGITIMATE` examples to test false-positive behavior

---

*Document version: 0.1 — Day 1 draft.*
