# CLAUDE.md — Antioch Building Materials Wiki

## Project Purpose

This is a GitHub wiki (`antiochbuilding-wiki.wiki`) for Antioch Building Materials. Its goal is to document internal business processes for onboarding new employees. The content philosophy is **deep links**: every complex process chains downward through increasingly specific pages so a reader can follow a topic from high-level concept all the way to ground-level detail (e.g., raw material sourcing and delivery logistics).

## Audience

New employees and trainees. Write clearly, assume no prior industry knowledge, and link aggressively to related pages.

## Platform: GitHub Wiki

- This repo IS the wiki. Each `.md` file is a wiki page.
- Page titles are derived from filenames: hyphens become spaces, e.g., `Concrete-Mixes-Pittsburg.md` → "Concrete Mixes Pittsburg".
- `Home.md` is the wiki landing page.
- Internal links use standard markdown: `[Page Title](Page-Title)` (filename without `.md`).
- GitHub wiki does NOT support subdirectories — all pages live at the root level. Use naming conventions to group related pages.

## File Naming Convention

`{Topic}-{Subtopic}-{Qualifier}.md`

Examples:
- `Concrete-Mixes-Pittsburg.md` — index of all Pittsburg mix designs
- `Mix-3000001006.md` — individual mix design page (Mix ID as identifier)
- `Material-Sand-Orca.md` — raw material page
- `Supplier-Cemex-Cement.md` — supplier/delivery page

Always use Title-Case-With-Hyphens. Never use spaces or underscores in filenames.

## Content Hierarchy (Deep Link Structure)

The intended drill-down chain for concrete is:

```
Home.md
└── Concrete-Mixes-Pittsburg.md        ← index of all Pittsburg mixes
    └── Mix-{MixID}.md                 ← individual mix design page
        └── Material-{Name}.md         ← ingredient/raw product page
            └── Supplier-{Name}.md     ← sourcing, delivery, and logistics page
```

Each level links DOWN to the next and UP to its parent.

## Primary Data Source: mixespitt.csv

Located at `mixespitt.csv` in the repo root. Contains 557 Pittsburg concrete mix designs exported from the batching system.

### CSV Columns

| Column | Description |
|---|---|
| Category | Usually empty; occasionally groups mixes |
| Mix ID | Unique alphanumeric ID (e.g., `300000006`) — use as the page identifier |
| Mix Name | Human-readable name (e.g., "3 sack sand slurry") |
| Mix Type | Always "Final Mix 1" |
| Current | `true`/`false` — whether this mix is still active |
| Method | Design method: `ACI`, `Manual`, or `Other` |
| Concrete Type | Usually "Normal" |
| Design Strength | Target PSI (0 means no strength requirement, e.g., slurries) |
| Required Strength | Override if set |
| Auto-Required | Boolean |
| Auto-Predicted | Boolean |
| Predicted Active | Boolean |
| Modified | Date last modified |
| Calculated | Date last calculated |
| Last Sent | Date last sent to batch plant |
| Send To Batch | Boolean |

### Key Patterns in the Data

- **Slurries**: Low-sack mixes (0–3 sack), 0 PSI design strength, sand-based.
- **Structural mixes**: Higher sack counts, 2500–5000+ PSI, used for building elements.
- **Specialty**: CTB (cement treated base), CIDH (cast-in-drilled-hole), popcorn (no-fines).
- **Suffix codes in Mix ID**: The last digits often encode aggregate type and admix (e.g., `006` = sand slurry base, `004` = popcorn, `000X` = neat cement). Decode these as we learn more.
- **Inactive mixes**: `Current: false` mixes should still get pages but marked as "no longer in use."

## Individual Mix Page Template

When creating pages for each mix from the CSV, use this structure:

```markdown
# {Mix Name} — Mix ID {Mix ID}

| Field | Value |
|---|---|
| Mix ID | {Mix ID} |
| Type | {Mix Type} |
| Method | {Method} |
| Concrete Type | {Concrete Type} |
| Design Strength | {Design Strength} PSI |
| Status | Active / Inactive |
| Last Modified | {Modified} |
| Last Sent to Batch | {Last Sent} |

## Description

[Brief description of what this mix is used for, when to use it, any notable characteristics.]

## Ingredients

| Material | Role | Link |
|---|---|---|
| [Material Name] | [Cement/Aggregate/Admix/Water] | [Material-Page] |

## Notes

[Any special handling, common job types, customer notes, etc.]

## See Also

- [Concrete Mixes Pittsburg](Concrete-Mixes-Pittsburg) — back to index
- [Related Mix Name](Mix-{RelatedID})
```

## Concrete-Mixes-Pittsburg.md — Index Page

This page should be a searchable index table of all 557 mixes, organized by type or sack count, with links to each individual mix page. Group by category or mix family where useful.

## Workflow for Generating Mix Pages from CSV

The task is to create one `.md` file per row in `mixespitt.csv`. Steps:
1. Parse CSV — use Python or shell script in the working directory.
2. For each row, generate a file named `Mix-{MixID}.md` using the template above.
3. Populate Concrete-Mixes-Pittsburg.md with a full index table.
4. Commit in logical batches (e.g., by mix family or sack range).

Scripts and one-off tools can live anywhere outside the wiki repo — do not commit tooling to the wiki itself.

## Planned Topic Areas (from Home.md)

- **Concrete**: Mix Designs, Materials, Color, Additives, Pricing Calculations, Brentwood vs Pittsburg differences
- **Ready Mix Trucks**: Series 97–122 (multiple series)
- **Maintenance Intervals**
- **Bottom Dumps**: Units 33–46
- **Asphalt Oil Deliveries**: Legacy
- **Cement / Fly Ash / Slag Hauling**
- **Heavy Equipment**
- **Asphalt**: CHASCO, Legacy (ASTEC Hardware, TC-II, WM-2000)

## Style Guidelines

- Use plain language. No jargon without a definition or link.
- Every page needs a "See Also" section with upward and lateral links.
- Tables over bullet lists when presenting structured data.
- Keep pages focused — one mix, one material, one supplier per page.
- Date format: YYYY/MM/DD (matches the batching system export format).
- PSI values as plain numbers with "PSI" suffix, no commas.
