---
name: marketing-compliance
description: Banking marketing compliance intelligence. Use when reviewing marketing content, advertisements, website copy, emails, or social media posts for regulatory compliance. Triggers on questions about UDAAP, FDIC, NCUA, Reg DD, Reg Z, TILA, Equal Housing, SAFE Act, or deposit/lending advertising rules for banks and credit unions.
---

# Marketing Compliance Knowledge

You have access to the `clarid-compliance` MCP server with the following tools for checking marketing content:

- **check_compliance** — Check any marketing content (ads, website copy, brochures) against all applicable regulations
- **check_email_compliance** — Check email marketing content with email-specific rules (CAN-SPAM, frequency disclosures)
- **check_social_compliance** — Check social media posts with platform-specific character/format constraints
- **generate_disclosures** — Generate required regulatory disclosures for a given product, channel, and context
- **compliance_summary** — Get a summary of recent compliance check results and trends

## Regulatory Framework

### UDAAP (Unfair, Deceptive, or Abusive Acts or Practices)
- **Unfair**: Causes substantial injury not reasonably avoidable and not outweighed by benefits
- **Deceptive**: Misleading representation or omission likely to mislead a reasonable consumer
- **Abusive**: Materially interferes with consumer's ability to understand terms, or takes unreasonable advantage of consumer's lack of understanding, inability to protect their interests, or reliance on the institution

Common UDAAP violations in marketing:
- Burying material terms in fine print
- Using "free" when conditions apply without clear disclosure
- Implying guaranteed approval
- Misleading savings claims without substantiation
- Bait-and-switch tactics (advertising terms not actually available)

### FDIC / NCUA Membership
- Banks must display "Member FDIC" on all advertising mentioning deposits
- Credit unions must display "Federally insured by NCUA" or the NCUA logo
- Non-deposit products must include "Not FDIC Insured", "No Bank Guarantee", "May Lose Value"
- Digital ads need membership statement visible without scrolling

### Equal Housing
- "Equal Housing Lender" text or logo required on all residential lending advertising
- Equal Housing Opportunity logo/text required for housing-related services
- Fair Housing Act prohibits discriminatory language in ads (race, color, religion, sex, handicap, familial status, national origin)

### Regulation DD (Truth in Savings)
- APY must be stated using the term "annual percentage yield" (not just "APY" alone on first reference)
- If an interest rate is advertised, APY must also be stated with equal prominence
- Bonus rates: must disclose when the bonus expires and the rate after expiration
- Minimum balance requirements to earn the stated APY must be disclosed
- Fees that could reduce earnings must be disclosed
- "Free" checking: cannot use if any maintenance fee or minimum balance fee applies

### Regulation Z (Truth in Lending) / TILA
- If any trigger term is used, full disclosure is required:
  - **Trigger terms**: specific payment amount, number of payments, period of repayment, finance charge amount
  - **Required disclosures when triggered**: APR, repayment terms, loan amount
- APR must be expressed as "annual percentage rate" with equal or greater prominence than other rate info
- Variable rate: must disclose that rate may vary and any caps
- Introductory/promotional rates: must state duration and post-promotional rate
- "As low as" rates: must state criteria for qualifying

### SAFE Act (NMLS)
- Individual MLO NMLS numbers required on loan advertising by specific originators
- Company NMLS number should appear on institutional lending ads
- State-specific requirements may apply

## Channel-Specific Rules

### Email Marketing
- All deposit/lending rules apply plus:
- CAN-SPAM compliance: physical address, unsubscribe mechanism, accurate subject lines
- Disclosures must be in the email body (not just linked)
- Pre-header text cannot be misleading

### Social Media
- Character limits don't excuse omitting required disclosures
- If full disclosure can't fit, ad must link to a landing page with full terms
- Paid endorsements/influencer content must disclose the relationship
- Comments/replies by the institution are considered advertising

### Website / Digital
- Required disclosures must be "clear and conspicuous" — visible without scrolling on the relevant page
- Pop-ups or expandable sections for disclosures are acceptable if clearly indicated
- Mobile-responsive disclosure presentation required

## How to Use the Tools

When checking marketing content:
1. Use **check_compliance** for general marketing materials (website, print, brochure)
2. Use **check_email_compliance** for email campaigns
3. Use **check_social_compliance** for social media posts
4. After checking, use **generate_disclosures** to get the exact disclosure language needed
5. Use **compliance_summary** to review patterns across multiple checks

Always present findings organized by severity: violations first, then warnings, then suggestions.
