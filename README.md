# C(n) — Block-Coprime Density

**Live:** https://wessengetachew.github.io/smith/

An interactive visualization suite by Wessen Getachew. A SoME submission.

---

## What is C(n)?

Fix a block of `n+1` consecutive integers. What fraction of all integers is
coprime to every member of that block?

For a single prime `p`, an integer is excluded when `p` divides it *and* `p`
divides one of the block's terms. Among any `n+1` consecutive integers, `p`
occupies exactly `min(n+1, p)` residue classes mod `p`, so averaging over
block positions gives a local survival factor of `1 − min(n+1, p)/p²`.
Multiplying over all primes gives the **raw density**:

```
D(n) = ∏ₚ (1 − min(n+1, p) / p²)
```

The site's primary object is the `ζ(2)`-normalized form:

```
C(n) = ζ(2) · D(n) = ζ(2) · ∏ₚ (1 − min(n+1, p) / p²)
```

`D` and `C` are tracked separately throughout, and the distinction matters:
`D(n)` is the convergence target for finite lattice counts, while `C(n)` is
the normalized constant the formulas are written in. Pages 9 and 10 depend on
getting this right.

At `n = 0` the block is a single integer and `C(0) = 1` exactly. The first
real step is:

```
C(1) = ζ(2) · ∏ₚ(1 − 2/p²) ≈ 0.530711820…
```

Neither factor is new. `ζ(2)` is [A013661](https://oeis.org/A013661), the
product `∏ₚ(1 − 2/p²) ≈ 0.322634098…` is
[A065474](https://oeis.org/A065474), and their product is
[A065469](https://oeis.org/A065469). Note that the *Feller–Tornier constant*
proper is a third object — `½(1 + ∏ₚ(1 − 2/p²)) ≈ 0.661317049…`,
[A065493](https://oeis.org/A065493) — and is **not** the same as either the
product or `C(1)`. The suite keeps all three apart deliberately.

Everything after that first step is where this project begins.

### Key results

- **Saturation mechanism.** The local factor `1 − min(n+1,p)/p²` freezes at
  `1 − 1/p` once `p ≤ n+1`. Each prime saturates the block in turn as `n`
  grows, producing the visible step structure. Verified with zero violations
  for all primes `p < 60` and all `n ≤ 79`.
- **Radical dependence.** In the multi-block generalizations, the density
  depends on a modulus only through its radical `rad(k)`. Confirmed
  numerically to 20 digits.
- **Mertens decomposition.** Splitting the product at `n`:
  `C(n) = ζ(2) · ∏_{p≤n}(1 − 1/p) · ∏_{p>n}(1 − (n+1)/p²)`, with
  `C(n)·ln n → ζ(2)·e^(−γ)`.

Original results are checked against known-answer tests using published OEIS
constants, plus cross-page consistency checks, before they stay. Claims that
failed numerically were cut or downgraded rather than hedged — two full pages
were removed outright during the audit for exactly this reason.

`C(n)`, the multi-block `C(n₁,…,n_k)`, the character-twisted `C_χ(n)`, the
block-coprimality framing, the lift-dynamics visualization, and the prime
spiral are original constructions. The classical results they build on —
Euler, Dirichlet, Riemann, Mertens, Farey, Ford, Stern–Brocot,
Hardy–Littlewood, Ramanujan, Gauss, Cayley, Franel–Landau — are credited
page by page in the in-app **Credits** panel on Page 2.

---

## Where to start

**Page 1 (`index.html`) is the guided walkthrough.** It builds the formula
piece by piece into a live working table with nothing hidden. Read it first.

**Page 2 (`page2.html`) is the full explorer** — the same mathematics with
every control exposed. It's the heaviest page in the suite and assumes you
already know what `C(n)` is.

Every page carries a **☰ Contents** button in the top bar listing all fifteen
pages with what each one covers, plus the animated Opener. Links open in the
same tab.

---

## The suite

| Page | File | What it is |
|---|---|---|
| **1** | `index.html` | **How C(n) Works** — guided walkthrough. The derivation, piece by piece, into a full live working table |
| **2** | `page2.html` | **C(n) — Block-Coprime Density** — the main explorer. Six lattice views, live Euler-product calculator, Goldbach / π(x) / prime-gap overlays |
| **3** | `page3.html` | **Color & Label Modes** — reference codex for all 34 color and label modes used across the suite, each a function of `(r, M, n)`, with live swatches and typeset definitions |
| **4** | `page4.html` | **The Prime Filter** — an *exact*, finite Eratosthenes sieve for one fixed block anchor `M`, contrasted against the `M`-averaged asymptotic density used everywhere else |
| **5** | `page5.html` | **Gap Diagonal Identity** — diagonal strips of the lattice have exact coprime density `φ(g)/g`, extended to block-coprimality |
| **6** | `page6.html` | **Strip Correlations** — how the diagonal strips of Page 5 fail to be independent, and why that's the same mechanism that forces `min(n+1,p)` into the formula |
| **7** | `page7.html` | **C(n₁,n₂)** — two independent blocks at once. Twin, cousin and sexy-prime presets; at `n=0` the correlation ratio becomes the exact finite picture behind prime gaps |
| **8** | `page8.html` | **C(n₁,…,n_k)** — the k-block generalization, connected to prime constellations and brute-force verified. 3D Ring view stacked by block-1 depth |
| **9** | `page9.html` | **C_χ(n)** — Dirichlet-character-twisted density, replacing `ζ(2)` with a genuine `L(2,χ)`, linked live to its Euler product |
| **10** | `page10.html` | **Farey & Unit Circle** — ten representations of the unit circle, plus a spectral-correlation panel against GUE, Poisson, and actual ζ zeros |
| **11** | `page11.html` | **Farey Summatory Function** — Mertens' summatory totient applied to Farey sector intervals. Exact / Hybrid / Formula toggle: brute force against closed form, side by side |
| **12** | `page12.html` | **The Prime Spiral** — one fixed prime's residue traced across rings of growing modulus, winding `r ≡ ±p (mod M)`. Explicitly *not* the Ulam spiral. Also the clearest explanation of the radial view's coordinates |
| **13** | `page13.html` | **Gauss Circle ↔ Farey Sector Bridge** — the lattice-point decomposition `N(R) = 1 + 4A + 4D + 8O`, in 2D and 3D |
| **14** | `page14.html` | **ζ(½ + it) — Critical-Line Spiral** — root-finds ζ zeros live via Riemann–Siegel `Z(t)`, not from a stored list |
| **15** | `page15.html` | **Sector-Graded Farey Discrepancy** — grades the Franel–Landau sum (RH-equivalent growth rate) by sector. A fraction's sector index turns out to be its first continued-fraction partial quotient |

---

## Page 2 — the explorer in detail

Six interchangeable lattice views on one canvas:

| View | What it shows |
|---|---|
| **Grid** | Raw `(r, M)` residue lattice, `G×G` |
| **Ring** | Concentric modular rings, one per `M`. Ring `M` sits at radius ∝ `M`; a point's angle is `θ = 2πr/M` with `1 ≤ r < M`, drawn where `gcd(r,M) = 1`, so ring `M` carries exactly `φ(M)` points |
| **Farey** | Residues plotted by their reduced fraction `r/M` |
| **Lift** | Prime-spiral overlay, `r → r mod (M+1)`, with mirror symmetry σ and a `±n` path tracer |
| **Gauss** | Gaussian-integer lattice, `a + bi` |
| **Cayley** | Conformal map `Γ(z) = (z−1)/(z+1)` — a Smith chart repurposed as pure lattice geometry |

Around the canvas:

- **Goldbach overlay** — live even-number decompositions plotted on the lattice
- **Asymptotic / Finite Π toggle** — switch the live formula between the true
  infinite product and a truncated partial product at a chosen `p_k`, with
  `C(n)`, `D(n)`, and block/saturation statistics all updating together
- **Export pipeline** — 2K/4K/8K PNG (true powers of two), plus multi-view
  composite export
- **Canvas-only fullscreen** — the entire control stack relocates into the
  fullscreened canvas so nothing is stranded off-screen
- **Send to Hero** — carries the opener's current state onto the page's hero
  section for a clean export shot
- **Status** — exports a full state report (parameters, theoretical vs.
  measured values, canvas snapshots) to PDF
- **Credits** and **Page Info** panels

---

## Tech

Single-file static HTML/CSS/JS per page. No build step, no framework, no
dependencies to install. MathJax for typeset formulas, Canvas 2D for every
lattice render. Typography is Cinzel / Spectral / JetBrains Mono; the color
language is gold / teal / coral throughout.

Open any page directly in a browser. Some features (exports, audio) hit
browser restrictions on `file://` URLs, so a local server is easier:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

---

## Author

Wessen Getachew — 2026

If this project is useful to you, a ⭐ on the repo is appreciated. Support for
new equipment is welcome via the PayPal / BTC links on Page 2.
