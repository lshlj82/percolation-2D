# Percolation on the square lattice

An interactive, single-file web demo of two-dimensional site percolation, based on lecture notes by Sang Hoon Lee, which follow K. Christensen and N. R. Moloney, *Complexity and Criticality* (2005). It simulates the transition as the occupation probability *p* changes, measures the critical exponents from its own data, checks the scaling relations between them, explores the fractal geometry of clusters, and walks through real-space renormalization.

Everything runs in the browser. There is no build step, no server and no dependencies beyond an optional web font.

## Running it

Open `index.html` in any modern browser (Chrome, Edge, Firefox or Safari).

To publish it with GitHub Pages, push this repository, then go to **Settings → Pages**, choose **Deploy from a branch**, and select the branch and the root folder. The page will be served at `https://<user>.github.io/<repository>/`.

## What the page contains

**Live lattice.** An L × L lattice (64 to 512) redrawn as you drag *p*, with every cluster colored or only the largest one highlighted. Readouts show the filled fraction, clusters per site, whether a cluster spans top to bottom, the largest-cluster share *P*, the mean cluster size χ, the correlation length ξ and the distance from *p*<sub>c</sub>.

**Order parameters across *p*.** Averaged runs for L = 16 to 128, with L = 256 available on request, plot the spanning probability *R*, *P*, χ and ξ against *p*. Log–log panels compare *P* ∝ (*p* − *p*<sub>c</sub>)<sup>β</sup> and χ ∝ |*p* − *p*<sub>c</sub>|<sup>−γ</sup> with the exact slopes.

**Measuring the exponents.** Finite-size scaling at *p*<sub>c</sub> gives 1/ν, β/ν, γ/ν, the fractal dimension *D* and ξ ∝ L. Periodic lattices give τ from the cluster-size distribution *n*<sub>s</sub>. Derived exponents (ν, β, γ, α, η, δ, σ) are listed next to the exact 2D values.

**Scaling relations.** Hyperscaling, Rushbrooke, τ = 1 + d/D, γ/ν = D(3 − τ), β/ν = D(τ − 2), ξ ∝ L and D − d = −β/ν, each evaluated with independently measured numbers.

**Data collapse.** Sliders for *p*<sub>c</sub>, 1/ν and the vertical exponent rescale *R*, *P*, χ or ξ so the curves for all sizes fall onto one scaling function.

**Fractal geometry of clusters.** On a separate 512 × 512 lattice:

- self-similarity: the largest cluster beside an enlarged corner of it
- window mass M(p;ℓ) ∝ ℓ<sup>D</sup> and density P(p;ℓ) = M/ℓ<sup>2</sup>, with the crossover from fractal to uniform at ℓ ≈ ξ
- cluster size against radius of gyration, s ∝ R<sub>s</sub><sup>D</sup>
- the crossover function m(ℓ/R<sub>s</sub>) for single finite clusters
- the scaling function m<sub>∞</sub>(ℓ/ξ) above *p*<sub>c</sub>
- *D* from five methods, and the relations D = 1/(σν) and D − d = −β/ν for one dimension, the square lattice and the Bethe lattice

**Real-space renormalization.**

- repeated coarse-graining of a lattice with a chosen block rule, each stage rescaled to the same size
- the RG map R<sub>b</sub>(p) with its iteration and the flow between fixed points
- the fixed point p\* and ν ≈ log b / log R<sub>b</sub>′(p\*) for five rules: the chain (b = 3), the triangular lattice (b = √3), and three square-lattice rules
- a "whole lattice as one block" estimate that uses the simulated spanning probability R<sub>L</sub>(p) as the RG map with b = L

## Methods

| Topic | Approach |
| --- | --- |
| Cluster labeling | Union–find with union by size and path halving |
| Curves over *p* | Newman–Ziff algorithm: sites are added one at a time in random order, so one run covers every *p*. Results are convolved with the binomial distribution, which gives smooth curves and exact derivatives such as dR/dp. |
| Boundaries | Open boundaries for the sweep and the fractal lattice; periodic boundaries for *n*<sub>s</sub>, so edges do not cut clusters. |
| Spanning | A cluster touching both the top and bottom rows. |
| Mean cluster size and ξ | Sums over all clusters except the largest. ξ<sup>2</sup> = Σ 2R<sub>s</sub><sup>2</sup>s<sup>2</sup>n<sub>s</sub> / Σ s<sup>2</sup>n<sub>s</sub>. |
| Fits | Least-squares lines on log–log data, with standard errors where at least three points exist. |

Measured exponents are close to the exact values but not equal to them. The small lattice sizes carry corrections to scaling, and "Add more samples" reduces random noise but not that bias.

## Exact values for 2D percolation

| Quantity | Value |
| --- | --- |
| *p*<sub>c</sub> (square lattice, site) | 0.59274621 (numerical) |
| β | 5/36 |
| γ | 43/18 |
| ν | 4/3 |
| α | −2/3 |
| η | 5/24 |
| δ | 91/5 |
| τ | 187/91 |
| σ | 36/91 |
| D | 91/48 |

## Files

```
index.html   the complete demo (HTML, CSS and JavaScript in one file)
README.md    this file
```

## Performance

The size sweep and the extra lattices start shortly after the page loads and run in small chunks, so the page stays responsive. Including L = 256 or choosing a 512 × 512 view needs more memory and time, which matters mostly on phones.

## References

The fractal-geometry and renormalization sections follow lecture notes by Sang Hoon Lee, which are based on the key reference.

**Key reference.** K. Christensen and N. R. Moloney, *Complexity and Criticality*, Imperial College Press, London (2005). Chapter 1 covers percolation, including cluster numbers, the order parameter, fractal geometry, finite-size scaling and real-space renormalization; Appendices C and D cover homogeneous functions and fractals.

Methods and exact results:

1. M. E. J. Newman and R. M. Ziff, "Efficient Monte Carlo algorithm and high-precision results for percolation," *Phys. Rev. Lett.* **85**, 4104 (2000). The site-by-site sweep and the binomial convolution used for every curve over *p*.
2. M. E. J. Newman and R. M. Ziff, "Fast Monte Carlo algorithm for site or bond percolation," *Phys. Rev. E* **64**, 016706 (2001). Details of the algorithm and the value *p*<sub>c</sub> = 0.59274621.
3. R. E. Tarjan, "Efficiency of a good but not linear set union algorithm," *J. ACM* **22**, 215 (1975). Union–find, used for all cluster labeling.
4. M. E. Fisher and M. N. Barber, "Scaling theory for finite-size effects in the critical region," *Phys. Rev. Lett.* **28**, 1516 (1972). Finite-size scaling and data collapse.
5. M. P. M. den Nijs, "A relation between the temperature exponents of the eight-vertex and q-state Potts model," *J. Phys. A* **12**, 1857 (1979). Exact ν = 4/3 in two dimensions.
6. B. Nienhuis, "Critical behavior of two-dimensional spin models and charge asymmetry in the Coulomb gas representation," *J. Stat. Phys.* **34**, 731 (1984). Coulomb-gas derivation of the exact 2D exponents.
7. K. G. Wilson, "Renormalization group and critical phenomena. I," *Phys. Rev. B* **4**, 3174 (1971). The renormalization group.
8. P. J. Reynolds, H. E. Stanley and W. Klein, "Large-cell Monte Carlo renormalization group for percolation," *Phys. Rev. B* **21**, 1223 (1980). Using whole lattices as RG blocks.
9. D. Stauffer and A. Aharony, *Introduction to Percolation Theory*, 2nd ed., Taylor & Francis, London (1994). General background on percolation.

## Credits

Lecture notes: Sang Hoon Lee.

Created by Claude Opus 5.5.
