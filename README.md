# Sparse vs. Dense Retrieval — Paper

Working repository for:

> **Beyond Representation: Index Structure Limitations in Dense Retrieval**
> Alessandro Magnani — AMLDS 2026 (Osaka, Japan, July 21–23, 2026)
> Paper ID: **S0460**

## Status

- **2026-04-28** — Accepted to AMLDS 2026 (weak accept, overall scores mostly "Fair").
- **Deadline** — Final paper + registration form due to `amlds_conf@163.com` **by 2026-05-13**.
- **Target template** — `IEEEtran` conference class (downloaded from
  https://amlds.site/style/downloads/conference-latex-template.zip — local copy in
  `amlds_template/`).

## File layout

| File | Purpose |
|---|---|
| `main_AMLDS.tex` | **Working camera-ready copy** for the AMLDS submission. Edits go here. |
| `main.tex` | Pre-acceptance IEEEtran version (anonymous). Reference; do not edit. |
| `main_asse.tex`, `main_asse_old.tex` | Older ACM `acmart` variants. Reference only. |
| `main_2.tex`, `main_3.tex` | Earlier drafts. Reference only. |
| `references.bib` | Shared bibliography (currently not loaded — bibitems are inline in `main.tex`). |
| `figures/` | All paper figures (PNG). |
| `amlds_template/` | Official AMLDS / IEEEtran template + example PDF. |
| `acmart.cls` | Legacy ACM class (kept so old variants still compile). |

## What we are doing and why

### Step 1 — Get `main_AMLDS.tex` compiling under the official AMLDS template
The existing `main.tex` already uses `IEEEtran` `[conference,anonymous]`, so the
class is right. Known issues to fix before first compile:

1. **Duplicated `\end{document}` and duplicated `\bibitem` entries** at the tail of
   the file (paste leftover after the first `\end{document}` on line ~411). Will
   break compilation — must be removed.
2. **Unused packages** (`algorithm`, `algorithmic`) — no algorithm environment is
   used. Trim.
3. **De-anonymize** — replace `Anonymous Author(s)` author block with real author
   info for the camera-ready.
4. Verify all `\includegraphics` paths resolve against `figures/`.

### Step 2 — Address reviewer feedback
The single reviewer gave **weak accept**, with these criticisms:

| Reviewer point | Planned response |
|---|---|
| Hard to identify what is fundamentally new vs. revisiting standard definitions | Trim background re-derivations; add a short "Novelty" paragraph after the intro contributions list; explicitly mark what is new (indexing-bias formalism, centroid-dilution bound for rare tokens, dimensionality–rare-query interaction). |
| Reads like a collection of observations, not a unified argument | Restructure §3–§4 around a single thread: *representation is sufficient → index approximations are the bottleneck → "spear fishing" queries expose it*. Add transitions between subsections that reference the four testable predictions. |
| Experiments simple / under-described | Expand §4.1 Setup with: corpus sizes, query counts per subset, embedding training detail (trigram vocab size, projection seed), IVF/HNSW parameter sweeps (exact ranges), and a reproducibility note. |
| Significance unclear | Add a "Practical implications" paragraph to the discussion quantifying the gap (e.g. ID queries on Home Depot: Flat 0.56 → HNSW 0.29, ≈48 % relative drop) and what that means for production retrieval stacks. |

### Step 3 — Final formatting pass
- Page limit check (IEEEtran two-column).
- Camera-ready checks: caption format, removal of any guidance/template text,
  consistent reference style, no `\cite{}` red boxes.
- Export final PDF and prepare submission email.

## Change log
- *2026-05-11* — Repo initialized. `main_AMLDS.tex` created as a copy of
  `main.tex`. Working copy and reviewer-response plan recorded here.
