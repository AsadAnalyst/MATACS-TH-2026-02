# Design write-up

## 1. AI vs. rules

The admin creates and publishes a versioned category configuration. The system validates that weights total 100% and that every mandatory check and scoring scale is defined. After upload, ordinary code validates files, scans them, removes duplicates, hashes originals, and OCRs them into page-numbered text. AI then extracts criterion evidence into a fixed schema with short quotes and page references; it does not decide eligibility or assign scores. Deterministic rules evaluate mandatory checks, apply the configured scales, calculate totals, and sort eligible bids. This boundary uses AI for varied language and rules for decisions that must be consistent and auditable.

## 2. Consistency and explainability

A run pins the category configuration version, scoring-rule version, prompt/model version, and input file hashes. With the same extracted fields and versions, deterministic scoring and tie-breaking produce the same result; AI extraction can vary, so production should pin the model, use constrained output, validate it, and retain the original extraction. A rerun that produces different extraction is surfaced for comparison or human review rather than silently replacing the first result. Reviewers see each criterion's evidence quote and page, pass/fail/unclear state, component score, weight, total, flags, and tie-break outcome.

The brief does not define scales for weighted criteria, so these sample results use illustrative scales: price is linear from the lowest eligible bid (100) to the $260,000 ceiling (0); timeline is linear from 10 weeks (100) to 16 weeks (0); panel warranty is capped at 25 years and workmanship at 12 years, then averaged; experience is proportional up to 10 qualifying projects; and team/approach equally credits a named lead, crew, safety plan, and monitoring plan. Weighted components are summed and rounded to one decimal. Production admins would configure and version these scales before evaluating bids.

## 3. Human in the loop

A reviewer confirms bidder labels and category at upload, then reviews unclear or conflicting extraction, mandatory evidence, and flagged results before scoring is finalized. They can correct extracted fields, request clarification, exclude a bid, or override the ordering, each with a reason. Only an authorized person makes and records the final award decision; the tool never awards a contract.

The audit record includes original file hashes, extracted text and citations, raw AI output, prompt/model versions, configuration snapshot, rule outcomes, score breakdown, flags, timestamps, reviewer edits, clarification responses, override reasons, and final decision. Prior values remain available so a result can be reconstructed.

## 4. Changing criteria

Published criteria are immutable for an existing run. An admin edit creates a new version; completed scores retain their original configuration snapshot and are not silently changed. A reviewer can explicitly start a new run against the new version, which recalculates every proposal in that run consistently and preserves a link to the earlier result. The interface should show which version produced each ranking.

## 5. Risks and safeguards

- **Wrong extraction or OCR:** Require page-linked quotes, schema/type validation, and human review for low confidence, missing, or conflicting critical fields. Keep the source PDF available for comparison.
- **Made-up facts or prompt injection:** Permit only evidence found in proposal text; treat document instructions as untrusted, require citations, and do not let AI set scores or eligibility. The instruction in C's appendix is ignored.
- **Bias or inconsistent scoring:** Use admin-defined criteria and fixed, published scales; test across comparable bids and show component scores. Do not use protected traits or irrelevant writing style as criteria.
- **Unfair comparisons or manipulation:** Define treatment of taxes, options, partial bids, and scope before scoring; flag suspicious or conditional claims and require clarification. BrightPath's future subcontractor does not meet the stated bidder-licence requirement.
- **Cost, privacy, or service failure:** Set file and model-use limits, monitor spend, restrict access, encrypt and apply retention controls, and provide a manual review path when AI/OCR is unavailable. Never expose API keys in code.

## Sample ranking

A ranks first (93.8), with mandatory evidence and strong experience, price, schedule, warranties, and team plan. E ranks second (81.4), with a strong team and 12-year workmanship warranty, but a higher price and longer schedule than A. C ranks third (71.4): it passes mandatory checks and has strong experience and warranties, but its 14-week schedule and missing safety/monitoring details lower its score. D is flagged because its schedule is undetermined, so it cannot be fairly scored on timeline. B is ineligible because the bidder's own Ontario electrical contractor licence is not confirmed; its subcontractor would be selected only after award.