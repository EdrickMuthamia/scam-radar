# Scam Radar — Scam Category Definitions

**Version:** 0.1 (Day 1)

Each category is defined with enough detail to write detection rules and label dataset examples.

---

## How to Read This Document

For each category:
- **Attacker objective** — what the scammer wants
- **Typical target** — who they go after
- **Message structure** — how the message is usually built
- **Psychological techniques** — how they manipulate the victim
- **Common indicators** — signals that suggest this category
- **Suspicious language examples** — actual phrases to watch for
- **URL/link behavior** — how links are typically used
- **Distinguishing from legitimate** — what separates a scam from a real message

---

## 1. FINANCIAL_SCAM

**Attacker objective:** Trick the victim into sending money directly, paying a fake fee, or providing payment credentials.

**Typical target:** Anyone; often targets people who recently made a transaction or are expecting a payment.

**Message structure:**
- Claims a payment is pending, blocked, or requires a fee to release
- May reference a real-sounding transaction ID or amount
- Requests payment to unlock funds or complete a transfer

**Psychological techniques:**
- Greed (large sum waiting for you)
- Urgency (offer expires soon)
- Authority (pretends to be a financial institution)
- Reciprocity (you must pay a small fee to receive a large amount)

**Common indicators:**
- Payment request
- Transaction fee or activation fee
- Unrealistic financial reward
- Urgency
- Vague sender identity

**Suspicious language examples:**
- "Your funds of KSh 120,000 are ready for release. Pay a processing fee of KSh 500."
- "To receive your transfer, you must first verify your account with a KSh 200 activation fee."
- "Your payment has been held. Contact us immediately to release it."

**URL/link behavior:**
- Links to unofficial payment portals
- Links to Google Forms or similar free platforms collecting payment details

**Distinguishing from legitimate:**
- Legitimate financial institutions do not ask you to pay a fee to receive money
- Legitimate messages reference your actual account number or transaction reference
- Legitimate senders use verified shortcodes or official domains

---

## 2. JOB_SCAM

**Attacker objective:** Collect upfront fees (registration, training, uniform, background check) or harvest personal identity documents.

**Typical target:** Job seekers, recent graduates, unemployed individuals.

**Message structure:**
- Unsolicited job offer with unusually high salary
- Minimal or no interview process described
- Requests payment or personal documents to proceed

**Psychological techniques:**
- Hope and desperation (targets people actively seeking work)
- Authority (fake company name, fake HR department)
- Urgency (limited positions available)
- Social proof (hundreds of people already hired)

**Common indicators:**
- Unsolicited job offer
- Unrealistically high salary
- Request for upfront payment
- Request for ID documents via WhatsApp or email
- No verifiable company information

**Suspicious language examples:**
- "You have been selected for a KSh 80,000/month position. Pay KSh 1,500 registration fee to proceed."
- "Urgent hiring: no experience needed. Send your ID and KSh 500 to secure your slot."
- "Work from home and earn KSh 5,000 daily. Limited slots. Apply now."

**URL/link behavior:**
- Links to fake company websites with no verifiable registration
- Links to Google Forms collecting ID numbers and personal details

**Distinguishing from legitimate:**
- Legitimate employers do not charge candidates to apply or get hired
- Legitimate job offers come after an application or interview process
- Legitimate companies have verifiable registration and contact details

---

## 3. PRIZE_SCAM

**Attacker objective:** Collect a "processing fee" or "tax payment" to release a prize that does not exist, or harvest personal details.

**Typical target:** General public; often mass-distributed.

**Message structure:**
- Announces unexpected winnings
- Creates excitement and urgency
- Requests a fee or personal information to claim the prize

**Psychological techniques:**
- Excitement and greed
- Urgency (claim within 24 hours)
- Scarcity (you are one of only 3 winners)
- Authority (claims to be from a known brand or government lottery)

**Common indicators:**
- Unexpected reward
- Urgency to claim
- Request for fee to release prize
- No record of entering a competition
- Vague or fake organization name

**Suspicious language examples:**
- "Congratulations! You have won KSh 50,000 in our annual draw. Click here to claim."
- "You are our lucky winner. Pay KSh 300 tax to receive your prize."
- "Your number was selected. Respond within 24 hours or forfeit your winnings."

**URL/link behavior:**
- Links to fake prize claim pages
- Links that collect personal and payment information

**Distinguishing from legitimate:**
- Legitimate prizes do not require upfront payment
- Legitimate competitions require you to have entered
- Legitimate organizations are verifiable and do not contact winners via random SMS

---

## 4. BANK_IMPERSONATION

**Attacker objective:** Steal banking credentials, OTPs, or card details by pretending to be the victim's bank.

**Typical target:** Bank account holders; often targeted using partial account information to appear credible.

**Message structure:**
- Claims there is a problem with the victim's account (suspicious activity, blocked card, failed transaction)
- Creates urgency to act immediately
- Directs victim to a fake login page or asks them to call a fake number

**Psychological techniques:**
- Fear (your account is at risk)
- Authority (impersonates a known bank)
- Urgency (act now or lose access)

**Common indicators:**
- Impersonation of a known bank
- Account security alert
- Request for OTP, PIN, or password
- Link to a non-official domain
- Urgency

**Suspicious language examples:**
- "EQUITY BANK ALERT: Suspicious login detected. Verify your account immediately: [link]"
- "Your KCB account has been suspended. Call 0700-XXXXXX to restore access."
- "IMPORTANT: Your card has been blocked. Enter your PIN at [fake link] to unblock."

**URL/link behavior:**
- Domains that misspell the bank name (equitybank-ke.com vs equitybank.co.ke)
- Legitimate-looking login pages on unrelated domains
- HTTPS does not guarantee legitimacy — scammers use free SSL certificates

**Distinguishing from legitimate:**
- Legitimate banks never ask for your PIN, OTP, or full password via SMS or link
- Legitimate bank SMS comes from verified shortcodes, not random mobile numbers
- Legitimate bank domains are well-known and consistent

---

## 5. MOBILE_MONEY_SCAM

**Attacker objective:** Steal M-Pesa funds, harvest M-Pesa PINs, or trick victims into sending money to the attacker.

**Typical target:** M-Pesa users; extremely common in Kenya.

**Message structure:**
- Fake M-Pesa confirmation message (you received money — now send it back)
- Fake M-Pesa error (your transaction failed — resend)
- Fake Safaricom alert asking for PIN to restore service

**Psychological techniques:**
- Confusion (fake confirmation creates false belief that money was received)
- Authority (impersonates Safaricom or M-Pesa)
- Urgency (act now before the transaction reverses)

**Common indicators:**
- M-Pesa or Safaricom impersonation
- Request to send money back
- Request for M-Pesa PIN
- Fake transaction confirmation format
- Urgency

**Suspicious language examples:**
- "You have received KSh 5,000 from John. Please send back KSh 4,500 as it was sent in error."
- "SAFARICOM: Your M-Pesa PIN has expired. Enter your PIN at [link] to continue."
- "M-PESA ALERT: Transaction failed. Resend KSh 2,000 to 0712XXXXXX to complete."

**URL/link behavior:**
- Fake Safaricom portals
- Links that mimic M-Pesa transaction pages

**Distinguishing from legitimate:**
- Safaricom never asks for your M-Pesa PIN via SMS or link
- Legitimate M-Pesa confirmations come from the shortcode 22522
- If someone claims to have sent money by mistake, verify in your own M-Pesa statement before acting

---

## 6. PHISHING

**Attacker objective:** Harvest login credentials, personal information, or payment details via a fake website.

**Typical target:** Anyone with online accounts; often targets users of specific platforms (banks, social media, email).

**Message structure:**
- Claims there is an urgent problem with an account
- Provides a link to a fake login page
- Collects credentials when the victim logs in

**Psychological techniques:**
- Fear (account will be closed)
- Authority (impersonates a trusted platform)
- Urgency (verify within 24 hours)

**Common indicators:**
- Link to a non-official domain
- Request to log in or verify credentials
- Urgency
- Impersonation of a known platform

**Suspicious language examples:**
- "Your Google account will be suspended. Verify now: [fake link]"
- "Facebook security alert: unusual login. Confirm your identity: [fake link]"
- "Your Netflix payment failed. Update your billing details: [fake link]"

**URL/link behavior:**
- Domains that closely mimic the real platform (g00gle.com, faceb00k.com)
- Login pages served over HTTPS on unrelated domains
- URL shorteners hiding the real destination

**Distinguishing from legitimate:**
- Legitimate platforms send password reset links only when you request them
- Legitimate login pages are on the platform's own verified domain
- Legitimate platforms do not threaten immediate account closure via SMS

---

## 7. SCHOLARSHIP_SCAM

**Attacker objective:** Collect application fees, processing fees, or personal documents from students seeking scholarships.

**Typical target:** Students, recent graduates, parents of school-age children.

**Message structure:**
- Announces a scholarship or bursary the victim did not apply for
- Requests a processing fee or personal documents to proceed
- May impersonate a real university, government body, or NGO

**Psychological techniques:**
- Hope (life-changing opportunity)
- Authority (fake government or university branding)
- Urgency (deadline approaching)
- Scarcity (limited slots)

**Common indicators:**
- Unsolicited scholarship offer
- Request for upfront payment
- Request for personal documents via WhatsApp
- Vague or unverifiable organization
- Urgency

**Suspicious language examples:**
- "You have been selected for a KSh 200,000 government scholarship. Pay KSh 1,000 processing fee."
- "HELB bursary available. Send your ID and KSh 500 to register before Friday."
- "Congratulations! You qualify for a full scholarship. Click here to apply before slots run out."

**URL/link behavior:**
- Fake government or university websites
- Google Forms collecting personal information and payment details

**Distinguishing from legitimate:**
- Legitimate scholarships do not charge application or processing fees
- Legitimate scholarship communications reference a specific application you submitted
- Legitimate government bursaries are announced through official channels

---

## 8. ROMANCE_SCAM

**Attacker objective:** Build emotional trust over time, then request money for an emergency, travel, or investment.

**Typical target:** Lonely individuals, widows/widowers, people on dating platforms.

**Message structure:**
- Initial contact is friendly and flattering
- Relationship develops over days or weeks
- Eventually introduces a financial emergency or investment opportunity

**Psychological techniques:**
- Love bombing (excessive affection and attention)
- Isolation (encourages victim to keep the relationship secret)
- Manufactured crisis (medical emergency, travel problem, business opportunity)
- Reciprocity (I will pay you back / I will come to you soon)

**Common indicators:**
- Unsolicited romantic contact from unknown person
- Rapid escalation of emotional intimacy
- Claims to be abroad or in a difficult situation
- Request for money transfer
- Reluctance to video call or meet in person

**Suspicious language examples:**
- "I have never felt this way about anyone. I need your help — I am stuck at the airport."
- "My business deal is almost done. I just need KSh 30,000 to complete it and I will repay you double."
- "I want to come visit you but my passport is held. Can you send money for the fee?"

**URL/link behavior:**
- Less URL-dependent; primarily operates via messaging
- May share fake investment platform links in later stages

**Distinguishing from legitimate:**
- Legitimate romantic interest does not quickly escalate to financial requests
- Legitimate contacts are willing to video call and meet in person
- Legitimate people do not ask strangers for money transfers

---

## 9. ACCOUNT_TAKEOVER

**Attacker objective:** Gain access to the victim's account (bank, M-Pesa, email, social media) by stealing OTPs or passwords.

**Typical target:** Anyone with a valuable online account.

**Message structure:**
- Claims the victim's account requires verification
- Requests the OTP that was just sent to the victim's phone
- May impersonate a customer service agent

**Psychological techniques:**
- Authority (fake customer service agent)
- Urgency (your account will be locked)
- Confusion (creates a scenario where sharing the OTP seems necessary)

**Common indicators:**
- Request for OTP
- Request for password or PIN
- Impersonation of customer service
- Urgency
- Claim that sharing OTP is required to verify identity

**Suspicious language examples:**
- "This is Safaricom support. To verify your account, please share the OTP sent to your phone."
- "Your account is being accessed by someone else. Give us the code we just sent to stop them."
- "KCB security team: we need your OTP to reverse a fraudulent transaction on your account."

**URL/link behavior:**
- Less URL-dependent; primarily social engineering via call or message
- May include a link to a fake support page

**Distinguishing from legitimate:**
- No legitimate company will ever ask you to share an OTP, PIN, or password
- OTPs are one-time codes specifically designed to be known only by the account holder
- Legitimate customer service can verify your identity without your OTP

---

## 10. INVESTMENT_SCAM

**Attacker objective:** Collect investment funds that will never be returned, or recruit victims into a Ponzi scheme.

**Typical target:** People seeking financial growth; often targets those who have heard about cryptocurrency or forex trading.

**Message structure:**
- Promises unrealistically high returns with low or no risk
- May show fake screenshots of profits
- Requests an initial investment to get started
- May require recruiting others (Ponzi structure)

**Psychological techniques:**
- Greed (double your money in 7 days)
- Social proof (fake testimonials, fake screenshots)
- FOMO (limited time offer, others are already profiting)
- Authority (fake financial advisor or trading expert)

**Common indicators:**
- Unrealistic return promise
- Guaranteed profit claim
- Request for investment funds
- Urgency to invest now
- Recruitment incentive

**Suspicious language examples:**
- "Invest KSh 5,000 and receive KSh 15,000 in 3 days. Guaranteed."
- "Our forex trading bot has 98% accuracy. Join now before slots close."
- "I made KSh 200,000 last month. I can show you how. Send KSh 10,000 to start."

**URL/link behavior:**
- Fake investment platform websites with professional design
- Platforms that show fake account balances to encourage further deposits
- Withdrawal requests are always blocked by new "fees"

**Distinguishing from legitimate:**
- Legitimate investments carry risk and never guarantee returns
- Legitimate investment platforms are regulated and verifiable
- Legitimate financial advisors do not solicit clients via unsolicited SMS or WhatsApp

---

*Document version: 0.1 — Day 1 draft.*
