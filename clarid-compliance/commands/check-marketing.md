---
description: Check marketing content against banking compliance regulations (UDAAP, FDIC/NCUA, Reg DD, Reg Z, Equal Housing, SAFE Act)
argument-hint: [paste or describe the marketing content to check]
---

# Check Marketing Compliance

Check the provided marketing content for regulatory compliance issues.

## Instructions

1. Determine the content type:
   - If the content appears to be an **email**, use the `check_email_compliance` tool from the `clarid-compliance` MCP server
   - If the content appears to be a **social media post**, use the `check_social_compliance` tool
   - For all other content (website copy, print ads, brochures, scripts), use the `check_compliance` tool

2. Pass the full content text to the appropriate tool. If the user provided a file path, read the file first.

3. Present the results organized by severity:
   - **Violations** (must fix before publishing)
   - **Warnings** (should fix, regulatory risk)
   - **Suggestions** (best practice improvements)

4. For each finding, explain:
   - What regulation it relates to
   - Why it's an issue
   - How to fix it

5. After presenting findings, ask if the user wants to **generate required disclosures** for the content. If yes, use the `generate_disclosures` tool with the appropriate product type, channel, and context.

## Example Usage

```
/clarid-compliance:check-marketing

Open a high-yield savings account today and earn 5.00% on your balance!
Limited time offer. Some restrictions may apply.
```
