---
name: hmda-validation
description: HMDA LAR file validation for community banks and credit unions. Use when validating Home Mortgage Disclosure Act Loan Application Register files, reviewing HMDA edit checks, or preparing CFPB submissions. Triggers on questions about HMDA, LAR files, edit checks, CFPB filing, or mortgage data reporting.
---

# HMDA LAR Validation Knowledge

You have access to the `clarid-hmda` MCP server with the following tools for HMDA validation:

- **hmda_validate_lar** — Upload and validate a LAR file against CFPB edit checks (pipe-delimited text or CSV)
- **hmda_get_validation** — Retrieve detailed results for a previous validation by ID
- **hmda_list_validations** — List all validation runs with status and summary counts
- **hmda_get_edits** — Get specific edit failures for a validation, filterable by edit type and severity

## HMDA Edit Check Categories

### Syntactical Edits (S-series)
Verify file format and data types. These must all pass before validity/quality edits run.

| Edit | Rule |
|------|------|
| S300 | File must begin with Transmittal Sheet (record type 1) |
| S301 | Each LAR row must contain exactly the required number of pipe-delimited fields |
| S302 | Activity year must be valid 4-digit year |
| S303 | LEI must be exactly 20 characters alphanumeric |
| S304 | Loan/Application ID must not be blank or exceed 45 characters |
| S305 | Action Taken Date must be valid YYYYMMDD |
| S306 | Application Date must be valid YYYYMMDD or "NA" |
| S307 | Numeric fields must contain valid numbers (no letters, proper decimal format) |
| S308 | Enumerated fields must contain only valid code values |
| S309 | ULI check digit must be valid per Mod 97 algorithm |
| S310 | No duplicate ULIs within the file |

### Validity Edits (V-series)
Cross-field consistency checks. Common failures:

| Edit | Rule |
|------|------|
| V600 | If Action Taken = 1 (originated), Action Taken Date must be >= Application Date |
| V610 | If Construction Method = 2 (manufactured), Total Units must be <= 4 |
| V615 | If Loan Purpose = 1 (purchase) and Lien Status = 1 (first), CLTV must be present |
| V620 | If Reverse Mortgage = 1 (yes), Applicant Age must be >= 62 or "8888" |
| V625 | If Preapproval = 1, Action Taken must be 1, 2, or 8 only |
| V628 | If Business/Commercial Purpose = 1, Loan Purpose cannot be Home Improvement with Personal Property |
| V630 | If Action Taken = 6 (purchased), Preapproval must be 5 (not applicable) |
| V631 | If Loan Type = 2 (FHA), Interest Rate must be present (not "NA" or "Exempt") |
| V635 | Rate Spread must be numeric or "NA" or "Exempt" — cannot be negative |
| V636 | If Loan Type = 1 (conventional) and Lien Status = 1, and not Exempt, HOEPA Status must be present |
| V640 | If Action Taken = 3, 4, 5, 6, 7, denial reasons must follow allowed combinations |
| V642 | Ethnicity, Race, Sex fields: codes must not conflict (e.g., "not applicable" with specific values) |
| V643 | If Applicant Ethnicity = 4 (not applicable), Race must also be 7 (not applicable) |
| V644 | Income must be present if Action Taken = 1, 2, 3, 4, 5 (not for purchased loans or preapprovals) |
| V645 | Census Tract must be valid 11-digit FIPS code |
| V650 | Property value must be numeric or "NA" or "Exempt" |
| V660 | If Total Loan Costs or Origination Charges present, Loan Amount must be numeric |
| V670 | Multifamily Affordable Units cannot exceed Total Units |
| V680 | If NMLSR ID present, must be numeric and valid format |

### Quality Edits (Q-series)
Reasonableness and outlier checks — flagged for review, not automatic failures:

| Edit | Rule |
|------|------|
| Q600 | Income appears unusually high or low for the area |
| Q601 | Loan amount to income ratio is unusually high (> 10x) |
| Q602 | Rate spread is unusually high for the loan type |
| Q605 | Property value appears unreasonable for the census tract |
| Q606 | Application date is more than 2 years before action taken date |
| Q607 | Age of applicant appears unreasonable (< 18 or > 100) |
| Q608 | Same ULI appears in prior year submission (possible duplicate) |
| Q610 | Census tract has very few reported loans (possible wrong tract) |
| Q615 | Unusually high percentage of "Exempt" or "NA" values across fields |
| Q620 | Distribution of loan purposes differs significantly from prior year |
| Q625 | DTI ratio reported as "NA" or "Exempt" for originated purchase loans |
| Q630 | NMLSR ID does not match NMLS registry records |

### Macro Edits (M-series)
Aggregate file-level checks:

| Edit | Rule |
|------|------|
| Q634 | Total loan count differs from prior year by > 20% |
| Q635 | Percentage of originated loans differs significantly from prior year |
| Q636 | Average loan amount changed by > 20% from prior year |
| Q637 | Geographic distribution shifted significantly from prior year |
| Q638 | Demographic distribution shifted significantly from prior year |

## Validation Workflow

1. **Upload**: Use `hmda_validate_lar` with the LAR file content. The tool accepts pipe-delimited text (standard CFPB format) or CSV.
2. **Review Results**: The validation returns a summary with counts by edit type. Use `hmda_get_edits` to drill into specific failures.
3. **Fix & Revalidate**: After correcting issues in the LAR file, run validation again.
4. **Track History**: Use `hmda_list_validations` to see all runs and compare error counts across iterations.

## Key Guidance

- Syntactical edits must all pass before validity edits are evaluated
- Quality edits are flags for human review, not automatic rejections
- Macro edits compare against historical patterns and may require written explanation
- Common first-time issues: incorrect ULI check digits (S309), missing census tracts (V645), and date format errors (S305/S306)
