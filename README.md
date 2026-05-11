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

### Step 2 — Address reviewer feedback ✅ DONE (2026-05-11)
The single reviewer gave **weak accept**, with four criticisms. All four addressed:

| Reviewer point | Response in revised draft |
|---|---|
| Hard to identify what is fundamentally new vs. revisiting standard definitions | Sharpened the four contribution bullets and added a *What is new versus prior work* paragraph at the end of §1 contrasting our index-level analysis against Tay et al. and Fan et al.'s representation-level analyses. Trimmed §2.3/2.4 to remove the ScaNN bullet (not used) and shortened the Research-Gap rehash. Sharpened the §3 framing paragraph to state the three-step argument and explicitly list what is new (centroid-dilution bound, indexing-bias decomposition, four predictions). |
| Reads like a collection of observations, not a unified argument | Tagged §3.5 as `sec:predictions` and added explicit forward-references so each experiment in §4 maps to a numbered prediction. Each results subsection in §4.4 now opens with `**Prediction N (...)**`. |
| Experiments simple / under-described | Rewrote §4.1 with exact corpus sizes (HD: 54,667 unique products; MS MARCO Passage v1.1 validation: 82,360 passages flattened from 10,047 queries), exact query-subset construction rules (rare-token threshold = ≤5 documents — this fixed a paper/code inconsistency where the paper had said ≤10), embedder spec (HashingVectorizer with 2^18 buckets, SparseRandomProjection density 0.9 seed 42, two trigram modes), full IVF/HNSW sweep ranges, and a reproducibility note pointing at the released code. |
| Significance unclear | Rewrote the abstract to lead with the centroid-dilution bound + the 63%-vs-2% headline number. Added a *Practical implications* paragraph quantifying the gap from real Table II numbers and arguing for query-type-aware routing. |

### Step 2.5 — Numeric refresh against fresh experimental data
We discovered while writing §4.1 that the paper's prior Table II had numbers that did **not** match the actual `sweep_results.json` outputs in `dense_retrieval_limitation_exp/v3/output/`. Replaced with the real, verified numbers at $d{=}1024$ across-token trigrams:

| Dataset | Subset | Flat | IVF | HNSW | BM25 |
|---|---|---|---|---|---|
| HD | std | 0.327 | 0.314 | 0.321 | 0.447 |
| HD | id  | 0.874 | 0.590 | 0.327 | 1.000 |
| HD | rare| 0.751 | 0.642 | 0.619 | 0.878 |
| MS MARCO | std | 0.471 | 0.448 | 0.446 | 0.770 |
| MS MARCO | id  | 0.174 | 0.152 | 0.071 | 0.000† |
| MS MARCO | rare| 0.205 | 0.187 | 0.166 | 0.688 |

(† BM25 zero on MS MARCO ID is because Lucene's default analyzer splits the compound IDs `qid_pidx`. Reported honestly in the paper.)

TREC-COVID was run in the codebase but **excluded from the paper**: standard-query Recall@10 collapsed to ~0.001 with unsupervised trigram embeddings — a representational pathology unrelated to our index-bias thesis, and including it would have muddied the story.

The MS MARCO BM25 > dense result is now framed in the paper as a known representation limitation, not a contradiction — our claim is about the Flat→ANN gap and is invariant to absolute recall.

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
- *2026-05-11* — Reviewer-response revision pass (Step 2): sharpened intro
  novelty framing; trimmed background; reworked §3 framing + tagged predictions;
  rewrote §4.1 Setup with exact corpus / embedding / sweep details;
  replaced stale Table II with verified numbers from
  `dense_retrieval_limitation_exp/v3/output/`; fixed rare-doc threshold
  inconsistency (≤10 → ≤5); added quantified Practical-Implications paragraph;
  rewrote abstract. PDF now 7 pages.
