# Antioch Building Materials — Wiki Repo

Internal knowledge base for Antioch Building Materials. Hosted as a GitHub Wiki. See the [live wiki](../../wiki) for the user-facing content.

---

## Status

### ✅ Done

| Area | Detail |
|---|---|
| **Home page** | Topic outline with link to Pittsburg mix designs |
| **Concrete Mixes — Pittsburg** | Index of all 557 Pittsburg mix designs (sorted, linked) |
| **Mix design pages** | 557 pages in `concrete-mix-designs/` — 547 with full ingredient data (slump, air, W/CM, compressive strength, lb/yd³, volume) |
| **Raw material pages** | 61 pages in `raw_materials/` — one per material (Cement, Aggregates, Admixtures, Fibers, Water) |
| **Deep links** | Full chain: Home → Mix Index → Mix Design → Raw Material, with back-links from raw material pages to every mix that uses them |

### 🔲 Next Up

- Add supplier and delivery details to raw material pages
- Build out Brentwood mix designs (separate index + pages)
- Link raw materials to supplier pages (`suppliers/`)
- Flesh out Notes sections on mix pages (job types, special handling)
- Truck maintenance pages (Ready Mix series 97–122, Bottom Dumps 33–46)
- Asphalt section (CHASCO, Legacy ASTEC/TC-II/WM-2000)

---

## Directory Structure

```
/                               ← wiki root
├── Home.md                     ← landing page
├── Concrete-Mixes-Pittsburg.md ← mix design index (557 mixes)
├── concrete-mix-designs/       ← individual mix pages (Mix-{ID}.md)
├── raw_materials/              ← raw material pages (Material-{Name}.md)
└── CLAUDE.md                   ← conventions and project guide for AI-assisted editing
```

## Data Sources (not committed)

| File | Contents |
|---|---|
| `mixespitt.csv` | Mix index — IDs, names, design strength, method, status |
| `pittmixes.csv` | Full mix designs — ingredients, proportions, slump, W/CM |
| `rawmats.csv` | Raw material registry — IDs, groups, types |

## Regenerating Pages

```bash
python3 generate_mix_pages.py
```

Requires `mixespitt.csv`, `pittmixes.csv`, and `rawmats.csv` in the repo root.
