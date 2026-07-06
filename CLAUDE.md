# The Corporate Supplier Sustainability Portal 2026

## Identity
A public landing page that onboards Tier 1 suppliers into The Corporate's ESRS-aligned sustainability assessment programme, routing each supplier to an EcoVadis scorecard submission or an in-tool questionnaire.
Tier: 1 — public form, no login, no database (D2+A1)
Spec version governed: v2.0
Position: Standalone

## Session Protocol
At the start of every session:
1. Pull the latest from main before reading anything else.
2. Check docs/product-spec.md: if its version is newer than the "Spec version governed" line in this file, STOP. Tell the builder: "The spec has changed since this CLAUDE.md was written — re-run the Project Governor on the revised spec before building, or these rules may contradict it." Do not build against a stale CLAUDE.md.
3. Read PROGRESS.md in the project root — it is the current state of this build. If it is missing, recreate it with the structure at the end of this section, then continue.
4. Increment the session number and update the date in PROGRESS.md.
5. If "Notes for next session" has content: repeat the notes back to the builder, treat them as this session's priorities, then clear the section.
6. If this is session 1, run First Session Setup below before any build work.

Save point — after completing any module, feature, fix, or view:
1. Update PROGRESS.md: current state, remaining work, build decisions, known issues.
2. Commit and push to main.
3. Tell the builder in one line: "Save point committed: [what changed]."
Do not start the next piece of work before the save point is pushed. Never end a session without one — an ending session is a save point.

First Session Setup (session 1 only):
1. Create docs/ and move product-spec.md into it.
2. Confirm the-corporate-brand skill is still installed at .claude/skills/the-corporate-brand/SKILL.md (carried over from the v1.0 build). If missing, install it there.
3. Announce what moved, then commit and push before building anything.

PROGRESS.md structure (for the recreate rule): status header (Session / Last updated / Live URL), Current state, Last session (3–5 lines, replace each session), Remaining work (shrinking checklist), Build decisions (one line each), Known issues, Notes for next session.

## Commands
```
npm install
npm run dev
npm run build
```

## Tech Stack
React · Vite · Tailwind CSS · Netlify
Deployment: GitHub → Netlify, auto-deploys from main. Netlify MCP is not active — the builder connects the repo and deploys manually through the Netlify dashboard after each build; remind them before the first deploy.

## Arms
Export — browser only, no server function — (1) the unchanged blank questionnaire template, The_Corporate_Supplier_Questionnaire_2026.xlsx, downloaded from within Door 2; (2) a branded PDF summary of the supplier's submitted answers, generated client-side after either door's submission.

## Hard Rules
- No data of any kind ever leaves the browser. No network request stores, logs, or emails submission data — this is Acceptance Criterion 13 and is verifiable in the browser's network tab. Refreshing or closing the tab clears everything; nothing persists across sessions.
- This tool requires no external services and no API keys. If any external service is added in a future version, its keys must never appear in frontend code or a GitHub commit.

## Project Structure
```
/                     ← root: CLAUDE.md, PROGRESS.md only
/src
  /components
  /lib
/docs                 ← product-spec.md
/.claude/skills/the-corporate-brand/   ← brand skill
/public/assets        ← The_Corporate_Supplier_Questionnaire_2026.xlsx
```

## Brand
Brand is governed by the the-corporate-brand skill at .claude/skills/the-corporate-brand/SKILL.md (confirmed installed in First Session Setup). Invoke it for any UI or visual work, including the new views and the PDF.
Hard rules that hold even if the skill is not loaded:
- Backgrounds: Chalk (#F2F2F2), Linen (#EAE4D5), White (#FFFFFF) — never a Tailwind gray default
- Accent: Acid Lime (#C8F135), used sparingly and always against Ink (#000000), never directly on a light background
- Fonts: Playfair Display for headings, DM Sans 300 for body, DM Sans 500 for labels and emphasis
- Square corners, no shadows, no gradients. No blue links — underline plus Ink color only.

## Business Rules
- Landing page correction: bring it in line with this spec before anything else. Two side-by-side route cards (EcoVadis card, Questionnaire card). The EcoVadis card opens ecovadis.com in a new tab. The questionnaire card's button reads "Complete Questionnaire" and opens the Door Choice view. This replaces the yes/no decision tree and the mailto EcoVadis submission found in the current index.html — the spec is the source of truth, confirmed with the builder 6 July 2026.
- Door 1 (Guided Form): required-field validation blocks advancing to the next section and blocks final submission until every required field across all 7 sections is valid; errors shown inline at the field level. Free back-and-forth navigation between any visited section.
- Door 2 (Download & Upload): a structural mismatch on upload (wrong file, missing sheets, unexpected layout) fails the read outright with a clear error — no partial or best-effort mapping. A successful parse that is missing required answers is treated the same as a missing required field in Door 1: the Upload Review screen flags what's missing and blocks Submit until a corrected file is uploaded.
- S1 to S7 field structure is not enumerated in the spec. Derive it by reading The_Corporate_Supplier_Questionnaire_2026.xlsx at build time (sheet names, cell labels, answer types) and confirm the mapping with the builder before finalizing the guided form.
- PDF export: client-side only, styled per the-corporate-brand, one section per heading S1 through S7 in order, header with logo and "Supplier Questionnaire Submission," footer with submission date and which door was used, no cover page.

Out of scope — do not build:
- Persisted storage of submissions (a database, Tier 2/3)
- Supplier login or verification (requires A2/A3 and a database)
- Internal review dashboard for procurement/EHS
- Submission tracker (percentage of Tier 1 suppliers who have responded)
- Automated EcoVadis scorecard validation

## Reference Docs
Read before building the related part:
- docs/product-spec.md — full module specs, UI sections, logic, arm detail
- .claude/skills/the-corporate-brand/SKILL.md — full brand system
PROGRESS.md in the root is read at every session start per the Session Protocol.
