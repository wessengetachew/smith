# C(n) — Block-Coprime Density

**Live page 1 The Index.html:** https://wessengetachew.github.io/smith/

# Page 2
https://wessengetachew.github.io/smith/page2.html

# Page 3 
     # Color and Lables detailed 
https://wessengetachew.github.io/smith/page3.html



An interactive explorer for the block-coprime density function

$$C(n) \=\ \zeta(2)\prod_{p}\left(1-\frac{\min(n+1,\,p)}{p^{2}}\right)$$

— the natural density of integer pairs $(r, M)$ with $\gcd(r, M+j)=1$ for every $j = 0,1,\dots,n$, rescaled by $\zeta(2)$ so that $C(0)=1$ exactly. One Euler product governs the density for every block length; every view on the page is that product made visible.

$C(1) = \zeta(2)\cdot\prod_p(1-2/p^2) = \prod_p \frac{p^2-2}{p^2-1} \approx 0.530711820472$ ([OEIS A065469](https://oeis.org/A065469)) — an exact algebraic identity linking the block-coprime density at $n=1$ to the lift-survival constant.

## What's on the page

The entire site is **one self-contained HTML file** (~21k lines). Everything runs in the browser; the only external dependencies are MathJax, html2canvas, and Google Fonts (all CDN).

### Six lattice views

| View | Construction |
|---|---|
| **Grid** | Columns $r$, rows $M$; gold cells are block-coprime. WebGL2 shader with Canvas2D fallback. Farey barrier overlays ($r/M = k$), saturation diagonal, Ulam/Fermat/Farey-strip/log-M alternate projections |
| **Ring** | The lattice on concentric circles, residue $r$ at angle $2\pi r/M$; per-ring twist, DHGS reciprocal-spiral overlay ($\rho\theta = \text{const}$), prime spires, lift-arc connections |
| **+Lift** | Arcs $r \to r \bmod (M{+}1)$ between consecutive rings; teal = survives ($\gcd(r, M{+}1)=1$), coral = broken. Depth-gated by the current $n$ |
| **Farey** | Reduced fractions $r/M$ by height; mediant/barrier structure |
| **Gauss** | The analogous picture over the Gaussian integers |
| **Smith** | Polar layout $z = R(M)e^{i\theta}$ passed through the Cayley map $\Gamma(z) = (z-1)/(z+1)$ |

All views are live: drag $n$, zoom/pan, animate, run a reorderable view tour, copy a URL that restores exact state, or export any configuration as a 4K PNG.

### Below the explorer

- **Calculator** — asymptotic mode (full product with analytic tail correction, ~12 dp) and finite mode (partial product over the first $k$ primes; exact BigInt rationals, $C_P(n)$ displayed as an exact multiple of $\pi^2$)
- **Step-by-step derivation** — CRT factorization, local factors, saturation events at $n = p-1$, running products, per-$n$ modal for every data-table row
- **Data table** — $C(n)$, $D(n)$, ratios, saturation events, CSV export
- **Hardy–Littlewood connection** — the structural parallel between the $C(n)$ local factor $1 - \min(n{+}1,p)/p^2$ (2D, pairs) and the singular-series factor $(1-\nu_p/p)/(1-1/p)^k$ (1D, residues), sharing the exclusion count $\nu_p = \min(n{+}1, p)$; derivation modals for $C_2$, $2C_2$, $D_{\mathrm{FT}}$, $C_{\mathrm{FT}}$
- **Additive number theory** — Goldbach partition counts $R(N)$ vs. the Hardy–Littlewood prediction $\tfrac12\mathfrak{S}(N)\,\mathrm{li}_2(N)$; $\pi(x)$ vs. $\mathrm{Li}(x)$
- **Strip average** — the diagonal decomposition $A(G) = \frac{2}{G^2}\sum_{g=1}^{G-1}(G-g)\,\frac{\varphi(g)}{g} \to \frac{6}{\pi^2}$, block-extended to recover $D(n)$
- **Transcendental ladder** — $1/\zeta(k) = \prod_p(1-p^{-k})$ computed in exact BigInt fixed-point against 46-digit references; for even $k$, $\pi$ is recovered from the partial product via an integer $k$-th root

## Mathematical scope

The density statements on this page are **theorems** — the Euler products converge absolutely, the identities are exact, and every displayed constant is checked against OEIS ([A013661](https://oeis.org/A013661), [A065469](https://oeis.org/A065469), [A065474](https://oeis.org/A065474), [A065493](https://oeis.org/A065493), [A059956](https://oeis.org/A059956)). The prime-counting statements they sit next to (twin primes, Goldbach) are **conjectures**, and the page keeps that line explicit: consecutive-integer tuples are not admissible ($\mathfrak{S}=0$ formally at $p=2$), so the Hardy–Littlewood connection is structural — shared exclusion counts in different ambient dimensions — not an identity, and nothing here counts primes.

Classical results (Euler, Mertens, Feller–Tornier, Hardy–Littlewood, Farey/Ford geometry) are credited in the page's credits panel. The $C(n)$ framing, the block-coprime lattice geometry, and the derived identities are constructions by Wessen Getachew.

## Usage notes

- **Ground state:** set $n$ in the opener (or the calculator) and check *set ground state* to lock every view, table, and live value to that $n$.
- **Shareable state:** the Link button encodes view, $n$, zoom, pan, and overlays into the URL hash; opening the link restores it.
- **Exports:** 4K PNG per view, CSV for the data table / per-prime factors / inspected points, and a printable HTML state report.
- **Performance:** a 1.5M-prime sieve and the smallest-prime-factor table are built at startup (SPF deferred); $C(n)$ values warm in two stages so first paint isn't blocked. WebGL2 is used for the grid when available.

## Repository

Single deliverable: `index.html`. No build step, no server — open the file or serve it statically.

## License

© Wessen Getachew ([@7dview](https://twitter.com/7dview)) · wessengetachew.github.io
Code and text may be viewed and shared with attribution; please link back to the live page.


## Page 2 

# Gap Diagonal Identity — Page 2

Part of Wessen Getachew's C(n) block-coprime density research suite
([Page 2](https://wessengetachew.github.io/smith/page2.html)). This page explores the
lattice `{(r, M) : 1 ≤ r ≤ M ≤ G}` through the diagonals `|M − r| = g`, using the classical
identity

```
coprime density on {|M − r| = g}  =  φ(g) / g
```

as a geometric lens on C(n)'s structure.

## Core idea

For a fixed gap `g`, the pairs `(r, M)` on the diagonal `|M − r| = g` are coprime with
density exactly `φ(g)/g` — a direct consequence of Euler's totient function and the identity
`gcd(r, r+g) = gcd(r, g)`. The page treats the full lattice as a stack of these diagonal
strips and lets you explore how each one behaves individually, then extends the same idea to
block-coprimality (`gcd(r, r+g+j) = 1` for `j = 0, …, n`) via C(n).

The Theory panel (collapsible, under the 2D Lattice tab) walks through the four-step proof of
the base identity, the block-coprime extension, and an honest accounting of what's classical
versus what's a visualization choice — the per-strip decomposition is a close approximation
to C(n) at n > 0, not an exact identity, since the strips share prime factors and aren't
independent.

## Views

**2D Lattice tab**
- **Grid** — the raw `(r, M)` lattice, colored by coprimality/block-coprimality, with a movable
  diagonal-gap highlight.
- **Ring · Barrier · Spire** — a combined polar view: residues placed on concentric rings by
  modulus M, with barrier and lift-survival overlays.
- **ℤ[i]** — the same coprimality condition read as visible/invisible points from the origin in
  the Gaussian integers, alongside the classical visible-lattice-point density `6/π² + O(log G/G)`.
- **Ford** — Ford circles (radius `1/(2q²)` at each reduced fraction `p/q`) paired with a
  Stern–Brocot mediant tree over the same sectors.

Each sub-view shares the same `G` (grid size), `g` (active diagonal), `n` (block depth), and
color-mode controls, plus 2ⁿ presets and a Play-G animation that ping-pongs G between 2 and 128.

**3D Cube tab** — the analogous coprime lattice `gcd(x, y, z) = 1` in three dimensions, with
density `1/ζ(3) ≈ 0.83191` (Apéry's constant), rendered as an interactive point cloud with
rotation, zoom, slicing, and gradient-arrow overlays.

**Field tab (⬡)** — a continuous view of local coprime density:
- **Vault Split** — splits the field along the diagonal to compare regions directly.
- **Density Heatmap / Gradient Flow** — computes `D_R(r, M)`, the coprime density in an
  `R`-neighborhood of each cell (via a summed-area table for speed), and draws its gradient,
  which points away from the coprime-sparse diagonal `r = M` toward denser strips.

The Field theory panel includes attribution for the classical visible-lattice-point result
(Cesàro 1881, Sylvester 1883, Dirichlet 1849, Mertens 1874) and its refinement under the
Riemann Hypothesis (Bureaux–Enriquez 2016, arXiv:1612.03700), along with the Herzog–Stewart
(1971) result on non-coprime "invisible forest" blocks.

## Controls

- **Grid G** (2–1024) — lattice size, shared across all 2D sub-views.
- **g** — active diagonal gap; can be locked to `G/2` so it tracks G automatically.
- **depth n** — block-coprimality depth; C(n) is recomputed live and shown in the sticky nav bar.
- **Color mode** — over a dozen palettes (sector angle, gap band, residue, φ(M)/M density, lift
  survival, Möbius μ, GCD spectrum, Farey rainbow, and more).
- **Zoom / pan** — mouse drag and scroll, or the zoom slider, with view-specific max zoom.

## Exports

Every tab has a 4K PNG export (3840×3840) that renders the current view with a header, active
formula, and live statistics baked in — suitable for sharing or printing.

## Navigation

The sticky top bar links to **P1** (the main C(n) Block-Coprime Density page), the current
page (**P2**), and the **Opener** welcome/teaser view.

## Implementation notes

Single-file HTML/CSS/JavaScript, no build step or external dependencies beyond MathJax (for
formula rendering) and JetBrains Mono/Cinzel/Spectral webfonts. All math (gcd, totient, Möbius,
primality, the C(n) Euler product) is computed client-side with plain trial-division and
memoized where it's called repeatedly. Canvas rendering is DPR-aware and capped at 3× pixel
ratio to keep memory use reasonable on high-density displays.


