---
name: fair-lending
description: Fair lending risk screening for community banks and credit unions. Use when analyzing lending data for fair lending risk, disparate impact, denial rate disparities, pricing differences, or geographic redlining patterns. Triggers on questions about fair lending, ECOA, disparate impact, redlining, CRA, or lending discrimination analysis.
---

# Fair Lending Screening Knowledge

Fair lending analysis uses HMDA data and internal lending data to identify potential disparate treatment or disparate impact across protected classes. The `clarid-hmda` MCP server provides tools that support fair lending screening through HMDA data validation and analysis.

## Available Tools

- **hmda_validate_lar** — Validate LAR data which is the foundation for fair lending analysis
- **hmda_get_validation** — Retrieve validation details including demographic data quality flags
- **hmda_get_edits** — Get edit failures that may indicate fair lending data quality issues (e.g., missing demographic fields)

## Fair Lending Analysis Framework

### 1. Denial Rate Analysis
Compares denial rates across demographic groups for comparable loan products:

- **Metric**: Denial rate ratio = (denial rate for protected group) / (denial rate for control group)
- **Threshold**: Ratios above 1.5x generally warrant further investigation (FFIEC guidance)
- **Protected classes**: Race/ethnicity, sex, age (40+), national origin
- **Controls**: Same loan product, similar income band, same geographic area, same time period
- **Statistical test**: Fisher's exact test or chi-square for significance at p < 0.05

### 2. Pricing Analysis
Compares rate spreads and APRs across demographic groups for originated loans:

- **Metric**: Mean/median rate spread difference between protected and control groups
- **Threshold**: Differences > 25 basis points warrant investigation
- **Controls**: Credit score band, LTV band, loan amount band, loan type, lien status
- **Method**: Regression analysis controlling for legitimate pricing factors
- **Key fields**: Rate Spread (HMDA field), Interest Rate, Total Loan Costs, Origination Charges

### 3. Geographic Analysis (Redlining Risk)
Identifies potential geographic discrimination in lending patterns:

- **Metric**: Loan application and origination rates by census tract demographics
- **Indicators**:
  - Low penetration in majority-minority tracts compared to peer institutions
  - Marketing/branch footprint excludes minority neighborhoods
  - Denial rates significantly higher in minority tracts after controlling for credit factors
- **Data sources**: HMDA LAR data, FFIEC census tract demographics, peer institution comparison
- **CRA connection**: CRA assessment area should not arbitrarily exclude minority areas

### 4. Content Screening
Reviews marketing materials for fair lending implications:

- **Prohibited**: Language that discourages applications from protected classes
- **Prohibited**: Images/models that suggest preference for particular demographic groups
- **Required**: Equal Housing Lender logo/text on residential lending ads
- **Required**: Availability in all languages used in marketing (if Spanish ads exist, Spanish disclosures must be available)
- **Watch for**: Targeted digital advertising that excludes protected class zip codes or demographics

## HMDA Data Quality for Fair Lending

Quality of HMDA demographic data directly impacts fair lending analysis reliability:

| Field | Impact if Missing/Incorrect |
|-------|---------------------------|
| Race | Cannot perform race-based denial/pricing analysis |
| Ethnicity | Cannot identify Hispanic/Latino disparities |
| Sex | Cannot perform gender-based analysis |
| Age | Cannot identify age discrimination patterns |
| Income | Cannot control for income in analysis |
| Census Tract | Cannot perform geographic analysis |
| Rate Spread | Cannot perform pricing analysis |
| Denial Reasons | Cannot assess whether denials are legitimate |

HMDA validation edits V642, V643, and V644 specifically check demographic data completeness.

## Risk Indicators

High-risk patterns that warrant deeper investigation:

1. **Denial rate ratio > 2.0x** for any protected group in any product
2. **Pricing variance > 50 bps** after controlling for risk factors
3. **Application volume < 50%** of expected in majority-minority tracts
4. **Demographic data "not provided" rate > 30%** (may indicate discouragement)
5. **Exception pricing** disproportionately benefits non-minority borrowers
6. **Referred vs. direct applicants** show different demographic patterns

## Regulatory Context

- **ECOA (Equal Credit Opportunity Act)**: Prohibits discrimination in any aspect of a credit transaction
- **Fair Housing Act**: Prohibits discrimination in residential real estate transactions
- **CRA (Community Reinvestment Act)**: Requires institutions to serve all communities in their assessment area
- **HMDA (Home Mortgage Disclosure Act)**: Requires data reporting that enables fair lending analysis
- **Interagency Fair Lending Examination Procedures**: Framework used by FDIC, OCC, Fed, NCUA for examinations
