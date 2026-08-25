# TotoSlip — Product Proposal

**A personal dashboard for tracking TOTO bets, checking results automatically, and viewing your own number history.**

---

## 1. Problem

People who play TOTO regularly, especially with multiple bet slips across draws, run into a few recurring frictions:

- **Manual checking is tedious.** Comparing each slip against the winning numbers by hand, especially with several slips and system entries, is slow and error-prone.
- **Slips get lost or forgotten.** Paper slips pile up; it's easy to lose track of what you've bet and when.
- **No personal history.** There's no easy way to see your own betting patterns over time, how close you've come to a prize, or which numbers you tend to play.
- **No single place to look.** Draw results, your slips, and any notes about your strategy all live in different places (paper, memory, screenshots).

TotoSlip already solves manual entry and draw-checking. This proposal extends it to remove the two biggest remaining pieces of friction: **getting slips into the app**, and **giving the user useful insight once their history builds up.**

---

## 2. Proposed Solution

TotoSlip becomes a lightweight personal dashboard with four pieces:

### 2.1 Slip capture (scan or upload)
- **Scan a physical slip** using a phone camera. The app reads the marked numbers off a standard Singapore Pools TOTO slip image.
- **Upload a PDF or screenshot** (e.g. an e-Pay bet confirmation) and extract the bet numbers automatically.
- User confirms the extracted numbers before saving — OCR isn't perfect, so a quick review step prevents a misread slip from silently corrupting the record.

### 2.2 Automatic draw checking
- Already built: enter or import a draw result, and every saved bet is checked against it instantly, with the matched numbers highlighted and prize group shown.
- Extension: bulk-check all unresolved bets against the latest draw in one action, rather than one at a time.

### 2.3 "How close you are"
- For every bet, show the **best result across all draws it's been checked against** — not just win/no-win, but the actual match count (e.g. "4 of 6, missed by 2 numbers").
- Surface near-misses (5 matches, 4 matches) distinctly, since these are the results a player is most likely to want to review.

### 2.4 Personal dashboard: hot/cold numbers & history
- **Hot numbers**: numbers that have appeared most often in the draws you've logged.
- **Cold numbers**: numbers that haven't appeared in a while, relative to your logged draw history.
- **Your own patterns**: which numbers you personally play most, and how that compares to actual draw frequency.
- Simple charts: match-count distribution over time, number frequency, bets logged per month.

**Important framing for this section:** hot/cold numbers are a historical summary, not a prediction. Each TOTO draw is an independent, random event — a number's past frequency doesn't change its odds in the next draw. The dashboard will present this clearly as *"numbers that appeared often/rarely in your logged draw history"* rather than implying any predictive power, to avoid misleading users.

---

## 3. User Flow

1. User scans a slip or uploads a bet confirmation PDF → app extracts numbers → user confirms → bet saved.
2. User enters or imports a new draw result (manually, or by pasting the Singapore Pools results page).
3. App auto-matches all pending bets, shows prize group or closest miss for each.
4. Dashboard updates: hot/cold numbers, personal frequency chart, running history.

---

## 4. Technical Approach

| Piece | Approach |
|---|---|
| Slip/PDF scanning | Image or PDF upload → OCR (number-grid recognition tuned to the TOTO slip layout) → structured numbers, with a manual-correction step before saving |
| Draw results | Manual entry (current), with an option to paste/import from the official results page |
| Storage | Local-first (per-device) by default; optional account-based sync if cross-device access is wanted later |
| Dashboard | Computed client-side from the user's own saved bets and draws — no external data source needed beyond what the user has logged |

This can be built as an incremental upgrade to the existing TotoSlip app rather than a rewrite — slip scanning and the dashboard are additive features on top of the current bet/draw storage.

---

## 5. Phased Rollout

**Phase 1 — Foundation (done):** manual bet entry, manual draw entry, automatic match checking. ✅

**Phase 2 — Capture:** photo scan of physical slips, PDF upload for bet confirmations, confirmation step before saving.

**Phase 3 — Insight:** "how close you are" near-miss view, match-count history.

**Phase 4 — Dashboard:** hot/cold numbers, personal frequency charts, logged-history stats.

**Phase 5 (optional) — Sync:** account-based storage so bets and draws follow the user across devices.

---

## 6. Risks & Considerations

- **OCR accuracy on scanned slips.** Handwriting or a poor photo angle could misread a number. Mitigated by the confirm-before-save step in every capture flow.
- **Draw data accuracy.** Manually entered draw results need to be correct, since one wrong number affects all match-checking. A future "import from official results" option reduces this risk.
- **Framing of hot/cold numbers.** As above — this must be clearly labelled as historical/descriptive, not predictive, to keep the app honest about how lottery draws work.
- **Data privacy.** Bet history is personal; local-first storage keeps it on the user's own device unless they opt into sync.

---

## 7. Why This Is Worth Building

The core value isn't predicting numbers — it's removing friction from something players already do (tracking and checking their own bets) and giving them an honest view of their own history in one place, instead of scattered paper slips and manual comparisons.
