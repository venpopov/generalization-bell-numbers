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

The `biber` pass is not optional: without it no `.bbl` is written and biblatex silently renders
every citation as its raw bold key (`[bernstein1995]`) instead of a number, with an empty
bibliography.

### Troubleshooting: `biber` fails on recent macOS

TeX Live ships `biber` for macOS as a universal (x86_64 + arm64) binary that, at startup,
extracts its own arm64 slice by calling `lipo -extract_family`. Recent macOS releases dropped
that flag from `lipo`, so `biber` aborts with:

```
biber: extracting arm64 binary with lipo failed (wstatus=256)
```

Because the failure happens before any LaTeX pass, the build "succeeds" and the broken
citations are the only visible symptom. Fix it once per machine by installing a thin arm64
`biber` earlier on `PATH`:

```sh
lipo /usr/local/texlive/2025/bin/universal-darwin/biber -thin arm64 -o ~/bin/biber
chmod +x ~/bin/biber
```

Verify with `biber --version` (should print a version, not the `lipo` usage text). Adjust the
TeX Live year in the path if needed; on Apple silicon `~/bin` must precede the TeX Live bin
directory on `PATH`. To undo: `rm ~/bin/biber`.
