---
description: Screen HMDA data for fair lending risk indicators including denial rate disparities, pricing differences, and geographic patterns
argument-hint: [path to LAR file or validation ID]
---

# Fair Lending Screen

Screen HMDA LAR data for fair lending risk indicators.

## Instructions

1. Get the data:
   - If the user provided a **LAR file path**, first validate it using `hmda_validate_lar` from the `clarid-hmda` MCP server
   - If the user provided a **validation ID**, retrieve it with `hmda_get_validation`
   - Check for demographic data quality issues (missing race, ethnicity, sex, income fields) using `hmda_get_edits` filtered to V642, V643, V644 edits

2. Assess data quality for fair lending analysis:
   - Flag if demographic "not provided" rate exceeds 30%
   - Flag if census tract data is missing on more than 5% of records
   - Warn that analysis reliability depends on data completeness

3. Summarize fair lending risk indicators based on the validated data:

   **Denial Rate Analysis**
   - Compare denial rates across race/ethnicity and sex groups
   - Flag any denial rate ratio > 1.5x (protected group vs. control group)
   - Note sample sizes — small counts (< 20 applications) reduce reliability

   **Pricing Analysis**
   - Compare mean/median rate spreads across demographic groups for originated loans
   - Flag differences > 25 basis points
   - Note that full pricing analysis requires controlling for credit score, LTV, and loan amount

   **Geographic Patterns**
   - Identify census tracts with unusually low application or origination volumes
   - Cross-reference tract demographics for potential redlining indicators
   - Note any majority-minority tracts with zero or very few applications

4. Present findings as a risk summary:
   - **High Risk** — Patterns exceeding regulatory thresholds
   - **Moderate Risk** — Patterns approaching thresholds or with small sample sizes
   - **Low Risk** — No significant disparities detected
   - **Data Gaps** — Areas where analysis is limited by data quality

5. Recommend next steps based on findings (deeper statistical analysis, peer comparison, policy review).

## Example Usage

```
/clarid-compliance:fair-lending-screen C:\Users\Bobby\hmda\2025-lar.txt
```
