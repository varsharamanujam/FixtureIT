# FixtureIt — Badminton Fixture Generator (single‑file web app)

## Problem statement
Scheduling badminton tournaments is tedious: multiple courts, byes, rest gaps, and fairness constraints make manual planning error‑prone. Organizers also need clean outputs (PDF/CSV/images) to share or print.

## What this app is
Open `index.html` in a modern browser to:
- Generate fixtures for Round‑robin or Knockout (optional seeding)
- Configure courts, match duration, minimum rest, and start time
- View schedules as a Table or a Flowchart (rounds/bracket)
- Download exports:
  - **Download Flowchart**: JPEG image of the flow (no connectors, clean)
  - **Download Table**: PDF (multi‑page with repeating headers) or CSV
- Save/Load inputs in localStorage (no backend)

## Why it helps
- Automates pairing and scheduling with standard, transparent algorithms
- Enforces minimum rest and avoids court double‑booking
- Produces portable outputs for sharing/printing
- Runs entirely offline

## Quick start
1. Open `index.html`.
2. Enter teams (one per line).
3. Choose format (Round‑robin/Knockout; tick “Seeded” if needed).
4. Set courts, match duration, rest, and start time.
5. Click **Generate Schedule**.
6. Use the **View** toggle (Table/Flowchart).
7. Exports:
   - **Download Flowchart** → JPEG
   - **Download Table** → PDF or CSV

Tip: Use **Save**/**Load** to persist your inputs for later sessions.

## Views and exports
### Table view
- Columns: `#`, `Round`, `Match`, `Team A`, `Team B`, `Court`, `Start`, `End`
- PDF export: landscape, repeating headers, avoids row splits
- CSV export: spreadsheet‑friendly

### Flowchart view
- Cards per round; exports omit connectors for readability
- Flowchart can be downloaded even when the Table tab is active (rendered off‑screen just for export)

## Scheduling logic (high‑level)
### Round‑robin (Circle method)
- `N` teams → `N−1` rounds (even `N`) or BYE inserted (odd `N`)
- Each round pairs opposite teams after rotation

### Knockout
- Pads to next power‑of‑two with BYEs
- Seeds by listed order if “Seeded”; otherwise shuffles
- Later rounds reference “Winner of R#‑M#”

### Time/court assignment
- Greedy across courts, respecting minimum rest per team
- Avoids court double‑booking
- For Knockout, enforces a round‑gap based on rest

## Constraints supported
- Multiple courts
- Match duration (minutes)
- Minimum rest (minutes)
- Start date/time
- Automatic BYEs (round‑robin odd teams; knockout padding)

## Troubleshooting
- **“pairs.forEach is not a function”** → generate the schedule first (Round‑robin uses the circle method).
- **Flowchart download on Table tab** → supported; if you see empty output, click **Generate Schedule** and try again.
- **Printed table misses rows** → use **Download Table → PDF**, then print the PDF.
- **Time strings wrap oddly** → the PDF export paginates better; you can also widen print margins.

## Browser support
Latest Chrome/Edge/Firefox/Safari. No server required. PDF libraries are loaded from CDNs when needed.

## Project layout
- `index.html` — entire app (UI, logic, exports). Open directly in a browser.

## Roadmap ideas
- Optional connectors in exports (toggle)
- Double‑elimination and hybrid group→KO
- Daily windows/blackouts, per‑venue constraints
- Drag/drop edits with re‑validation
- Team tags/color‑coding
