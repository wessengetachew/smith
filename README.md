# C(n) — Block-Coprime Density

**Live page:** https://wessengetachew.github.io/smith/

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
