# AMLDS 2026 — 15-minute Presentation

Source: `slides.tex` (Beamer, 16:9 aspectratio, default+seahorse theme).
Compile with:

    pdflatex slides.tex && pdflatex slides.tex

## Talk outline (14 slides, ~15 minutes)

| # | Slide | Time |
|---|---|---|
| 1 | Title | 30 s |
| 2 | Why this talk + headline 63%-vs-2% number | 1 min |
| 3 | Two camps (sparse vs dense) + the gap prior work leaves | 1 min |
| 4 | "Spear-fishing" queries (definition + the three subsets) | 1 min |
| 5 | Theory: centroid dilution bound | 2 min |
| 6 | Experimental setup + methodological justification | 1.5 min |
| 7 | Headline table (Recall@10 across grid) | 1.5 min |
| 8 | Indirect evidence: IVF nlist sensitivity | 1 min |
| 9 | Direct evidence: per-query centroid signal (40× collapse) | 2 min |
| 10 | The empty-result rate (zero-Recall@10) | 1 min |
| 11 | "But supervised encoders!" — H rebuttal | 2 min |
| 12 | Production implications + recommendations | 1 min |
| 13 | Takeaways | 1 min |
| 14 | Q&A | — |

Figures live in `figures/` (copied from the paper's `figures/`).
Code/experiments link in slide 13: `github.com/alemagnani/sparse-dense-paper`.
