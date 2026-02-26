---
description: Validate a HMDA LAR file against CFPB edit checks (syntactical, validity, quality, and macro edits)
argument-hint: [path to LAR file or paste LAR data]
---

# Validate HMDA LAR

Validate a Home Mortgage Disclosure Act Loan Application Register file against CFPB edit checks.

## Instructions

1. Get the LAR data:
   - If the user provided a **file path**, read the file contents
   - If the user **pasted data**, use it directly
   - The LAR file should be pipe-delimited (standard CFPB format) or CSV

2. Use the `hmda_validate_lar` tool from the `clarid-hmda` MCP server to validate the data.

3. Present the validation summary:
   - Total records processed
   - Counts by edit type: Syntactical (S), Validity (V), Quality (Q), Macro (M)
   - Overall pass/fail status

4. If there are failures, use `hmda_get_edits` to get the details. Present them grouped by edit type:
   - **Syntactical edits** first (these block further validation)
   - **Validity edits** (cross-field consistency issues)
   - **Quality edits** (flagged for review, not automatic failures)
   - **Macro edits** (file-level aggregate checks)

5. For each edit failure, explain:
   - Which records are affected (by row number or ULI)
   - What the edit checks for
   - How to correct the data

6. If the user wants to track progress, mention they can use `hmda_list_validations` to see all validation runs and compare error counts across iterations.

## Example Usage

```
/clarid-compliance:validate-lar C:\Users\Bobby\hmda\2025-lar.txt
```
