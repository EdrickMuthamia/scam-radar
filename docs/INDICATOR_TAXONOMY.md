# Scam Radar — Indicator Taxonomy

**Version:** 0.1 (Day 1)

This document defines every indicator the scoring engine can detect, organized by group.

An indicator is a signal that contributes to risk. No single indicator proves fraud. The engine combines multiple indicators to produce a score.

---

## Indicator Format

Each indicator has:
- **Code** — used in dataset `indicators` field and scoring engine
- **Name** — human-readable label shown in output
- **Description** — what it means and when it applies
- **Base weight** — default contribution to risk score (adjustable)
- **Notes** — edge cases, false-positive risks

---

## Group A — Linguistic Indicators

These are detected from the text content of the message.

| Code | Name | Description | Base Weight | Notes |
|---|---|---|---|---|
| `URGENCY` | Urgency language | Message creates time pressure: "immediately", "now", "within 24 hours", "expires today" | 10 | Very common in legitimate messages too; weight is intentionally low |
| `THREAT` | Threat language | Message threatens negative consequences: "account will be closed", "legal action", "arrested" | 15 | Stronger signal than urgency alone |
| `UNEXPECTED_REWARD` | Unexpected reward | Claims the recipient has won, been selected, or is receiving an unsolicited benefit | 15 | Must not have entered a competition |
| `FINANCIAL_INCENTIVE` | Financial incentive | Specific monetary amount offered as reward or prize | 10 | Combine with UNEXPECTED_REWARD for higher confidence |
| `PRESSURE` | Pressure language | Pushes the recipient to act without thinking: "don't miss out", "act before it's too late" | 10 | Often co-occurs with URGENCY |
| `SECRECY` | Secrecy request | Asks recipient to keep the communication confidential | 20 | Strong signal; legitimate organizations rarely ask for secrecy |
| `CREDENTIAL_REQUEST` | Credential request | Asks for password, PIN, OTP, or security code | 25 | Very strong signal; no legitimate service asks for this via message |
| `UNUSUAL_GRAMMAR` | Unusual grammar | Message contains grammar errors, awkward phrasing, or inconsistent formatting unusual for the claimed sender | 8 | Weak signal alone; combine with others |
| `UNSOLICITED_OFFER` | Unsolicited offer | Recipient did not request the service, job, prize, or opportunity being offered | 12 | Context-dependent; combine with other signals |
| `RECRUITMENT_INCENTIVE` | Recruitment incentive | Offers rewards for recruiting others (Ponzi/pyramid signal) | 18 | Strong signal for INVESTMENT_SCAM |
| `GUARANTEED_PROFIT` | Guaranteed profit claim | Claims investment returns are guaranteed or risk-free | 20 | No legitimate investment guarantees returns |
| `UNREALISTIC_RETURN` | Unrealistic return | Promises returns that are implausibly high (e.g., triple your money in 3 days) | 20 | Combine with PAYMENT_REQUEST for high confidence |

---

## Group B — Financial Indicators

These relate to money movement, fees, or financial promises.

| Code | Name | Description | Base Weight | Notes |
|---|---|---|---|---|
| `PAYMENT_REQUEST` | Payment request | Asks the recipient to send money | 20 | One of the strongest signals |
| `UPFRONT_FEE` | Upfront fee | Requires payment of a fee before receiving a benefit (prize, job, scholarship) | 22 | Legitimate prizes and jobs do not charge fees |
| `PROCESSING_FEE` | Processing fee | Calls the fee a "processing", "activation", or "registration" fee | 18 | Variant of UPFRONT_FEE |
| `WITHDRAWAL_FEE` | Withdrawal fee | Claims a fee is needed to withdraw or release funds | 22 | Classic advance-fee fraud signal |
| `INVESTMENT_PROMISE` | Investment promise | Promises financial returns from an investment | 12 | Alone is not sufficient; combine with UNREALISTIC_RETURN |
| `TRANSACTION_REVERSAL` | Transaction reversal request | Claims money was sent by mistake and asks for it to be returned | 20 | Classic M-Pesa scam pattern |

---

## Group C — Identity Indicators

These relate to who the sender claims to be.

| Code | Name | Description | Base Weight | Notes |
|---|---|---|---|---|
| `IMPERSONATION` | Impersonation | Claims to be a known organization (bank, telco, government) without verification | 20 | Must be combined with other signals; legitimate orgs also identify themselves |
| `FAKE_AUTHORITY` | Fake authority | Claims government, legal, or regulatory authority to pressure compliance | 18 | "This is the Kenya Revenue Authority" in an unsolicited message |
| `FAKE_COMPANY` | Fake company representative | Claims to represent a company that cannot be verified | 15 | Requires domain/sender verification to confirm |
| `UNVERIFIED_SENDER` | Unverified sender | Message comes from a regular mobile number rather than a verified shortcode or official domain | 10 | Context-dependent; friends and family use regular numbers |
| `ACCOUNT_THREAT` | Account threat | Claims the recipient's account is at risk, suspended, or compromised | 15 | Combine with IMPERSONATION for bank/telco scam pattern |

---

## Group D — URL and Link Indicators

These are detected from URLs present in the message.

| Code | Name | Description | Base Weight | Notes |
|---|---|---|---|---|
| `SUSPICIOUS_URL` | Suspicious URL | URL does not match the claimed sender's known domain | 20 | Requires a known-domain reference list |
| `MISSPELLED_DOMAIN` | Misspelled domain | Domain name is a close misspelling of a legitimate organization (equitybank-ke.com) | 22 | Strong signal |
| `UNUSUAL_TLD` | Unusual TLD | Domain uses an unexpected top-level domain for the claimed organization (.xyz, .tk, .ml) | 15 | Context-dependent; some legitimate services use unusual TLDs |
| `EXCESSIVE_SUBDOMAINS` | Excessive subdomains | URL has many subdomains to obscure the real domain (login.verify.safaricom.fake.com) | 18 | The real domain is the last two parts before the TLD |
| `URL_SHORTENER` | URL shortener | Link uses a URL shortening service (bit.ly, t.co, tinyurl) hiding the real destination | 12 | Common in legitimate marketing too; weight is moderate |
| `UNRELATED_DOMAIN` | Unrelated domain | Login or payment page is hosted on a domain unrelated to the claimed organization | 20 | Strong signal |
| `FREE_HOSTING` | Free hosting platform | Link goes to a free platform (Google Forms, Typeform, Glide) collecting sensitive information | 15 | Legitimate organizations use their own infrastructure for sensitive data |

---

## Group E — Behavioral Indicators

These relate to what the message is asking the recipient to do.

| Code | Name | Description | Base Weight | Notes |
|---|---|---|---|---|
| `BYPASS_NORMAL_PROCESS` | Bypass normal process | Asks recipient to skip standard procedures: "don't go to the branch, just send here" | 18 | Strong signal |
| `PLATFORM_SWITCH` | Platform switch request | Asks recipient to move conversation to another platform (WhatsApp, Telegram) | 12 | Common in romance and investment scams |
| `OTP_REQUEST` | OTP request | Explicitly asks for a one-time password or verification code | 25 | Extremely strong signal; no legitimate service does this |
| `PASSWORD_REQUEST` | Password request | Asks for account password | 25 | Extremely strong signal |
| `PIN_REQUEST` | PIN request | Asks for M-Pesa PIN, bank PIN, or ATM PIN | 25 | Extremely strong signal |
| `DOCUMENT_REQUEST` | Document request | Asks for ID, passport, or other identity documents via informal channel | 15 | Legitimate employers use formal HR processes |
| `UNEXPECTED_REQUEST` | Unexpected request | The request is something the recipient did not initiate or expect | 10 | Weak alone; combine with other signals |

---

## Scoring Rules

### Combination Multipliers

Some indicator combinations are stronger together than their individual weights suggest. These multipliers are applied after summing base weights:

| Combination | Multiplier | Rationale |
|---|---|---|
| `CREDENTIAL_REQUEST` + `IMPERSONATION` | ×1.3 | Classic account takeover pattern |
| `UPFRONT_FEE` + `UNEXPECTED_REWARD` | ×1.3 | Classic advance-fee fraud |
| `SUSPICIOUS_URL` + `IMPERSONATION` | ×1.2 | Classic phishing pattern |
| `PAYMENT_REQUEST` + `URGENCY` + `THREAT` | ×1.2 | High-pressure financial fraud |
| `UNREALISTIC_RETURN` + `PAYMENT_REQUEST` | ×1.3 | Investment scam pattern |

### Score Cap

The final score is capped at 100. The formula is:

```
raw_score = sum of base weights for detected indicators
adjusted_score = raw_score × applicable_multiplier (if any)
final_score = min(adjusted_score, 100)
```

### Minimum Score Floor

A message with zero indicators scores 0. There is no artificial floor.

---

## Indicators That Require Context

These indicators should NOT be applied mechanically. They require context before contributing to the score:

| Indicator | Context Required |
|---|---|
| `URGENCY` | Only meaningful when combined with a financial or credential request |
| `FINANCIAL_INCENTIVE` | Only meaningful when the reward is unsolicited |
| `IMPERSONATION` | Only meaningful when the sender cannot be verified as the claimed organization |
| `UNVERIFIED_SENDER` | Not meaningful for personal messages between known contacts |
| `URL_SHORTENER` | Not meaningful in isolation; many legitimate marketing messages use shorteners |

---

## Indicators NOT in This List (Intentionally Excluded)

The following are NOT indicators on their own:
- Mentioning a company name (legitimate companies mention themselves)
- Containing a link (legitimate messages contain links)
- Mentioning money (legitimate financial messages mention money)
- Using the word "urgent" (legitimate messages use this word)
- Being in Swahili (language is not an indicator of fraud)

---

*Document version: 0.1 — Day 1 draft.*
