# The Attention Timeline

A single-page web app that explains every attention mechanism from the session **in the order it actually launched** — starting from standard scaled dot-product attention, with each later mechanism presented as a response to a limitation of what came before. For every entry: what it **buys**, what it **gives up**, and when you'd actually **choose** it.

It's one self-contained `index.html` (no build step, no dependencies beyond a Google Fonts link), so it hosts anywhere.

## Run it

Open `index.html` in a browser. That's it.

## Deploy it (for the live link)

- **Netlify:** drag this folder onto the deploy drop-zone at app.netlify.com/drop.
- **Vercel:** run `vercel` inside this folder (or import the repo at vercel.com/new).
- **GitHub Pages:** push to a repo, then Settings → Pages → deploy from the default branch.

## What's in it

1. **Standard attention** — an interactive 5-stage pipeline (`Q·Kᵀ → scale → mask → softmax → ×V`) run on the tokens *I / am / Batman / lmao*, then the three "bills" that seed the rest of the timeline (memory, compute, order).
2. **The timeline** — 17 mechanisms in launch order, colour-coded by the problem family they attack, filterable by family.
3. **The arc** — a plot of every mechanism by release date and family, so you can watch the field's priorities move.
4. **Sources** — the table below, plus the honest footnotes.

---

## Chronology & sources

Every date was checked against the primary paper's arXiv record or the original author post, not taken from memory. Dates are the field where a confident agent is most likely to be wrong.

| # | Mechanism | First appeared | Family | Primary source |
|---|-----------|----------------|--------|----------------|
| 1 | Scaled dot-product attention (+ sinusoidal PE) | Jun 2017 | foundation / position | Vaswani et al., *Attention Is All You Need* — [arXiv:1706.03762](https://arxiv.org/abs/1706.03762) |
| 2 | Absolute **learned** positional embeddings | May 2017 | position | Gehring et al., *ConvS2S* — [arXiv:1705.03122](https://arxiv.org/abs/1705.03122) (default in decoders via BERT, 2018) |
| 3 | Sparse Transformers (factorised/strided sparse) | Apr 2019 | sparsity | Child, Gray, Radford, Sutskever — [arXiv:1904.10509](https://arxiv.org/abs/1904.10509) |
| 4 | Multi-Query Attention (MQA) | Nov 2019 | cache | Shazeer, *One Write-Head is All You Need* — [arXiv:1911.02150](https://arxiv.org/abs/1911.02150) |
| 5 | Sliding-window (local) attention | Apr 2020 | sparsity | Beltagy, Peters, Cohan, *Longformer* — [arXiv:2004.05150](https://arxiv.org/abs/2004.05150) |
| 6 | Linear attention (*Transformers are RNNs*) | Jun 2020 | recurrent | Katharopoulos, Vyas, Pappas, Fleuret — [arXiv:2006.16236](https://arxiv.org/abs/2006.16236) |
| 7 | Delta rule in linear attention (Fast Weight Programmers) | Feb 2021 | recurrent | Schlag, Irie, Schmidhuber — [arXiv:2102.11174](https://arxiv.org/abs/2102.11174) |
| 8 | RoPE (Rotary Position Embedding) | Apr 2021 | position | Su et al., *RoFormer* — [arXiv:2104.09864](https://arxiv.org/abs/2104.09864) |
| 9 | ALiBi (Attention with Linear Biases) | Aug 2021 | position | Press, Smith, Lewis — [arXiv:2108.12409](https://arxiv.org/abs/2108.12409) |
| 10 | Grouped-Query Attention (GQA) | May 2023 | cache | Ainslie et al. — [arXiv:2305.13245](https://arxiv.org/abs/2305.13245) |
| 11 | Position Interpolation (PI) | Jun 2023 | position | Chen, Wong, Chen, Tian — [arXiv:2306.15595](https://arxiv.org/abs/2306.15595) |
| 12 | **NTK-aware** scaled RoPE | Jun 2023 | position | /u/bloc97, r/LocalLLaMA (community post — **no paper**) |
| 13 | YaRN | Aug 2023 | position | Peng, Quesnelle, Fan, Shippole — [arXiv:2309.00071](https://arxiv.org/abs/2309.00071) |
| 14 | Attention sinks (StreamingLLM) | Sep 2023 | cache | Xiao, Tian, Chen, Han, Lewis — [arXiv:2309.17453](https://arxiv.org/abs/2309.17453) |
| 15 | Multi-head Latent Attention (MLA) | May 2024 | cache | *DeepSeek-V2* — [arXiv:2405.04434](https://arxiv.org/abs/2405.04434) |
| 16 | DeltaNet (parallelisable) | Jun 2024 | recurrent | Yang, Wang, Zhang, Shen, Kim — [arXiv:2406.06484](https://arxiv.org/abs/2406.06484) |
| 17 | Gated DeltaNet | Dec 2024 | recurrent | Yang, Kautz, Hatamizadeh — [arXiv:2412.06464](https://arxiv.org/abs/2412.06464) |
| 18 | Native Sparse Attention (NSA) — DeepSeek "compressed sparse attention" | Feb 2025 | sparsity | Yuan et al. — [arXiv:2502.11089](https://arxiv.org/abs/2502.11089) |
| 19 | DeepSeek Sparse Attention (DSA, lightning indexer) | Sep 2025 | sparsity | *DeepSeek-V3.2-Exp* technical report |
| 20 | DroPE (Drop Positional Embeddings) | Dec 2025 | position | Gelberg et al., Sakana AI — [arXiv:2512.12167](https://arxiv.org/abs/2512.12167) |

**Honorable mention (in the app, deliberately not counted as a mechanism):** FlashAttention — Dao et al., May 2022 — [arXiv:2205.14135](https://arxiv.org/abs/2205.14135). It's the *same* softmax attention, exact, just an IO-aware kernel. It changed what's affordable, not what attention is.

**Precursor referenced in the DroPE card:** NoPE (No Positional Embedding) — Kazemnejad et al., May 2023 — [arXiv:2305.19466](https://arxiv.org/abs/2305.19466).

---

## Honest footnotes (and two corrections to the session material)

- **NTK-aware scaling has no paper.** It began as a Reddit post by `/u/bloc97` on r/LocalLLaMA (June 2023) and was written up later inside YaRN. Its "primary source" is a forum thread — worth stating rather than dressing up as a citation.
- **DroPE — corrected.** The class notes treated DroPE's mechanism as unverified. The real method (Sakana AI, Dec 2025) **drops positional embeddings entirely** after pretraining, turning the model into a **NoPE** model that relies on position implied by the causal mask, then briefly recalibrates at the original context length (before final annealing). "Dro" = *Drop*, not a rescaling of RoPE.
- **"Compressed Sparse Attention" = Native Sparse Attention.** DeepSeek's publicly documented mechanism is NSA (Feb 2025): compress-into-blocks + cheap top-k block selection + a sliding-window branch, natively trainable. The later DeepSeek-V3.2-Exp "Sparse Attention" (Sep 2025) adds a *lightning indexer* for the ranking step.
- **Couldn't verify from the notes.** `LightningLM V4`, the `DDDGDDDG` depth schedule, and `Memory Stream` don't map to a public primary source I could find, so the timeline is built on the underlying **published** mechanisms (DeltaNet, NSA, MLA, …) rather than those internal model names. The "RoPE on a subset of dims" detail attributed to a "V4" is a real property of DeepSeek's **decoupled RoPE** in MLA. Flagged per the brief's "if I've made one, catch that too."
- **Learned-absolute vs the Transformer.** Learned positional embeddings appear in ConvS2S (May 2017), ~a month before the Transformer (June 2017); the Transformer chose sinusoidal but reported learned as comparable, and BERT (2018) made learned-absolute the default. Treated as one 2017-era entry in the app.
