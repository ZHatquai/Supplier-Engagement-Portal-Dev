# PROGRESS — The Corporate Supplier Sustainability Portal 2026

> Claude Code: read this file at the start of every session, before touching anything. Update it at every save point. Replace content, do not append. History lives in git.

**Session:** 1 — first session governed by Project Governor
**Last updated:** 6 July 2026 — by Project Governor, pre-build
**Live URL:** v1.0 is already live on Netlify (URL not recorded in this repo's docs yet) — confirm and record the URL here after this build's deploy

## Current state
v1.0 exists and is live: a static HTML/CSS/JS single-page site (index.html) with EcoVadis and questionnaire routes. It was built and deployed before this project used Project Governor, so this is the first governed session, not a fresh build. As deployed, v1.0 does not match product-spec.md: it uses a yes/no decision tree ("Do you have a current EcoVadis Scorecard?") rather than two side-by-side route cards, and the EcoVadis path submits via a mailto link rather than opening ecovadis.com. Repo contains CLAUDE.md, PROGRESS.md, docs/product-spec.md, the-corporate-brand brand skill, index.html, and The_Corporate_Supplier_Questionnaire_2026.xlsx.

## Last session
None — this is the first governed session.

## Remaining work
- [ ] First Session Setup: create docs/, move product-spec.md, confirm the-corporate-brand skill installed at .claude/skills/, commit (see CLAUDE.md Session Protocol)
- [ ] Correct the landing page to match the spec: two side-by-side route cards, EcoVadis card opens ecovadis.com in a new tab, questionnaire button reads "Complete Questionnaire" and opens Door Choice
- [ ] Migrate the frontend from HTML/CSS/JS to React + Vite + Tailwind, preserving the corrected landing page content and all brand rules
- [ ] Build Door Choice — let the supplier pick Door 1 or Door 2, with a way back to the landing page
- [ ] Build Guided Form (Door 1) — derive the S1 to S7 field structure from the Excel asset, confirm the mapping with the builder, sequential navigation and validation
- [ ] Build Download & Upload (Door 2) — download the unchanged template, accept .xlsx or .csv upload, validate structure on read
- [ ] Build Upload Review (Door 2) — read-only summary of parsed answers, Submit or re-upload
- [ ] Build Confirmation Screen — shared by both doors, submission summary and Download PDF
- [ ] Wire the Export arm: client-side .xlsx/.csv parsing for Door 2, and client-side PDF generation on the Confirmation Screen, styled per the-corporate-brand
- [ ] Local test pass — full walkthrough of every view before deploying
- [ ] Acceptance criteria pass — verify all 15 criteria in spec Section 13 before deploy
- [ ] Deploy to Netlify — builder adds nothing (no env variables needed), confirms the deploy manually in the Netlify dashboard (Netlify MCP not active)

## Build decisions
None yet.

## Known issues
- v1.0 as previously deployed did not match product-spec.md (yes/no decision tree, EcoVadis submitted by email instead of linking to ecovadis.com). Confirmed with the builder on 6 July 2026 that the spec is authoritative; the landing page correction is the first item in Remaining Work above.

## Notes for next session
None.
