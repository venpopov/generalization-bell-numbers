# m-Bell and m-Stirling numbers: binomial transforms, hyper-Bessel functions, and moments of the Conway–Maxwell–Poisson distribution

This repository contains the manuscript and supporting computational material for a paper on a
generalization of the Bell numbers: the *m-Bell numbers*, sequences that shift left by *m* places
after *m* applications of the binomial transform, and the associated *m-Stirling* triangular arrays.

Highlights:

- The **m-Bell numbers** satisfy `B_{n+m} = Σ_k C(n,k) m^(n-k) B_k`. The case m=1 gives the
  classical Bell numbers (A000110); m=2 gives the "Bessel–Bell" numbers A007472, A351143, A351028.
- The **m-Stirling triangle** `Z(n+1,k) = m⌊k/m⌋ Z(n,k) + Z(n,k-1)` (m=2 case: OEIS
  [A383235](https://oeis.org/A383235)). The main structure theorem: its row sums give the composite
  m-Bell numbers and its residue-class row sums (k mod m) give the m primitive m-Bell sequences.
- Exponential generating functions are hypergeometric (hyper-Bessel) functions — modified Bessel
  functions for m=2 — with Dobiński-type formulas, dual first-kind triangles, generalized falling
  factorials, Lah-type companions, and two combinatorial models (parity-constrained urns and
  restricted permutation insertions).
- The m-Bell numbers govern the moments of the **Conway–Maxwell–Poisson distribution** with
  dispersion ν = m, exactly as the Bell numbers govern Poisson moments.

## Files

- `manuscript.tex` — the paper (compile with `pdflatex` + `biber`; requires `stmaryrd`, `tikz-cd`,
  `amsaddr`, `pdflscape`)
- `references.bib` — bibliography
- `notebooks/` — Mathematica notebooks with computational verification
- `supporting/` — standalone derivations from earlier drafts (superseded by the manuscript)

## Build

```sh
pdflatex manuscript.tex
biber manuscript
pdflatex manuscript.tex
pdflatex manuscript.tex
```
