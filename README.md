# DPDP Readiness Assessment

**Deloitte India | Enterprise Security**

A single-file, client-side assessment tool for the **Digital Personal Data Protection Act, 2023** and **DPDP Rules, 2025** (G.S.R. 846(E), notified 13 Nov 2025). Designed for security and privacy advisers to run in client conversations and pitches.

- No build step, no dependencies, no network calls.
- All data stays in the browser (answers are kept in `localStorage` for convenience; use **Reset** to clear).
- Safe to use with client information on a shared screen or offline.

## Run it

Open `index.html` in a browser, or publish with GitHub Pages (Settings, Pages, deploy from branch, root folder).

## How it works

1. **Applicability and classification** (s.3, s.10, Third Schedule): scope, role (fiduciary or processor), platform thresholds (e-commerce 2 crore users, social media 2 crore, gaming 50 lakh), children's data, SDF indicators. These switch controls on or off.
2. **38 controls** across 10 domains, each tied to a section or rule, with the evidence a CISO should ask for.
3. **Maturity scale** per control: 0 None, 1 Ad hoc, 2 Defined, 3 Operating and evidenced. N/A removes a control from scope.
4. **Output**: score, rating, per-domain bars, priority gaps, statutory penalty ceiling touched, countdown to the main obligations date, JSON export, print to PDF.

### Scoring

```
control points = weight x (maturity / 3)
domain score   = sum(points) / sum(weights)
overall score  = sum(points) / sum(weights) x 100     (answered, applicable controls only)
```

| Score | Rating |
|---|---|
| 80 and above | Strong |
| 60 to 79 | Established |
| 35 to 59 | Developing |
| below 35 | Critical |

**Critical-gap gate:** if any weight-3 control scores 0, the rating is capped at *Developing* regardless of the numeric score.

**Weights** reflect regulatory consequence: 3 for controls whose failure maps to the highest Schedule tiers or to core lawfulness (security safeguards, breach notification, consent proof, children, SDF duties); 2 for standard obligations; 1 for supporting or conditional controls.

**Penalty ceiling** shown is the highest Schedule tier among controls scored 0 or 1: INR 250 crore (security safeguards, including processor security clauses), 200 crore (breach notification, children), 150 crore (SDF), 50 crore (other). These are statutory maximums under s.33 and the Schedule, not predictions, and the Board must weigh the s.33(2) factors.

### Key dates (computed from the notification)

| Provision | In force |
|---|---|
| Rules 1, 2, 17-21 | 13 Nov 2025 |
| Rule 4 (Consent Managers) | 13 Nov 2026 |
| Rules 3, 5-16, 22, 23 | 13 May 2027 |

## Extending

All content lives in the `C` (controls) and `DM` (domains) arrays near the top of the script.

```js
["S3", 3, "Statement", "Legal ref", "Evidence to request", "optional condition: c | s | t"]
```

Tier overrides are in `TIER`. Add a control, adjust weights, or add a sector overlay (for example RBI, IRDAI, SEBI, CERT-In) by following the same pattern. Bump `VER` when the model changes so exported JSON stays traceable.

## Known limitations

- Self-reported maturity is only as reliable as the evidence behind it. The tool lists the evidence to request; it does not verify it.
- It does not decide whether an entity will be notified as a Significant Data Fiduciary; it only screens indicators.
- Cross-border conditions (s.16, Rule 15) and localisation (Rule 13(4)) depend on future government orders; update the model when issued.
- Sector regulation (banking, insurance, health, telecom) and overlapping laws (IT Act, CERT-In directions) are not scored.
- Section 17(3) exemptions (including for startups) are not applied, as the Rules do not currently notify any.

## Branding

The header uses a text-based wordmark (Deloitte with green dot, brand green `#86BC25`) as a placeholder. Before wider circulation, replace the `.logo` element in `index.html` with the official logo asset from the Deloitte brand centre and have the footer wording approved by Risk and Legal, since logo use and legal boilerplate are governed by Deloitte brand and risk policy.

## Disclaimer

Educational and advisory aid. It is not legal advice and does not determine or certify compliance. Validate against the notified Act, Rules and subsequent orders. Review with your firm's risk and legal functions before external distribution or branding.
