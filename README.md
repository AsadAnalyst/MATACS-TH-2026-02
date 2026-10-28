# MATACS · Associate Software Developer Assessment

**Name:** Asad Raza  
**Reference:** MATACS-TH-2026-02  

## Submission files

- [Process flow diagram](diagram/process-flow.png)
- [Design write-up](WRITEUP.md)
- [AI prompts](PROMPTS.md)
- [Expected ranking](ranking.json)
- [Optional offline prototype](prototype/run_triage.py)

Run the prototype from the repository root with `python prototype/run_triage.py`. It is an interactive offline walkthrough: press Enter to advance step by step, type `q` to quit, then inspect a proposal by entering A–E or type `r` to restart. It needs only Python 3.10+ and makes no network or API calls. Its local regex extraction demonstrates the workflow; it is not live AI extraction.

## AI tools

I used ChatGPT Codex to organize the design, draft the extraction and scoring prompts, and check that the sample ranking followed the stated criteria. I corrected its initial inclination to treat BrightPath as eligible because its subcontractor would be licensed: the mandatory rule requires the bidder's own Ontario electrical contractor licence to be held and stated in the proposal, so BrightPath is ineligible. I also treated the instruction embedded in Lakeview's appendix as untrusted proposal text, not an instruction to the review system.
