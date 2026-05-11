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
| `main_AMLDS.pdf` | Latest compiled PDF (regenerate with `pdflatex main_AMLDS.tex`). |
| `references.bib` | Shared bibliography (currently not loaded — bibitems are inline in the tex). |
| `figures/` | All paper figures (PNG). |
| `amlds_template/` | Official AMLDS / IEEEtran template + example PDF. |
| `old/` | Archived prior versions (`main.tex`, `main_asse*.tex`, `main_2/3.tex`, `acmart.cls`). Not built; kept for reference only. |

## What we are doing and why

### Step 1 — Get `main_AMLDS.tex` compiling under the official AMLDS template ✅ DONE (2026-05-11)
The existing `main.tex` already used `IEEEtran` `[conference,anonymous]`, so the
class was right. Fixes applied to `main_AMLDS.tex`:

1. Removed the duplicated `\end{document}` and duplicated `\bibitem` entries that
   were pasted after the first `\end{document}` (lines ~411+).
2. Removed unused `algorithm` / `algorithmic` packages.
3. Removed the `anonymous` class option and replaced the author block with
   *Alessandro Magnani, Independent Researcher, ale.magnani@gmail.com* (update
   the affiliation before sending the final).
4. Commented out the placeholder "Acknowledgments withheld" section.

Current state: compiles cleanly with `pdflatex main_AMLDS.tex` (no errors,
no undefined references), output is **6 pages**.

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
- *2026-05-11* — `main_AMLDS.tex` cleaned up: removed dup bibliography tail,
  unused algorithm packages, anonymous flag; added real author block.
  Compiles cleanly to a 6-page PDF.
- *2026-05-11* — Moved prior `main*.tex` variants and `acmart.cls` to `old/`
  so only `main_AMLDS.tex` is the active source.
