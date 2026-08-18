# C(n) — Block-Coprime Density

**Live page 1 The Index.html:** https://wessengetachew.github.io/smith/

**A SoME6 submission — interactive visualization suite by Wessen Getachew**

🔗 Live site: [wessengetachew.github.io](https://wessengetachew.github.io)

---

## What is C(n)?

Pick a random whole number, and a fixed modulus `M`. What's the probability that
it — and the `n` numbers right after it — all share no common factor with `M`?
That probability has a name, **C(n)**, and it drops at every step, with the
sharpest drops landing wherever a prime *saturates* the block:

```
C(n) = ζ(2) · ∏ₚ (1 − min(n+1, p) / p²)
```

It starts at certainty — `C(0) = 1`, exactly. The first real step lands on
`C(1) ≈ 0.530711…`, which is nothing mysterious: it's `ζ(2)` times the classical
Feller–Tornier product `∏ₚ(1 − 2/p²)` ([Feller & Tornier, 1932/33](https://oeis.org/A065469)).
Two known constants, one known answer — everything *after* that first step is
where this project begins.

A companion quantity, `D(n) = C(n)/ζ(2)`, gives the **raw density** (with the
`ζ(2)` normalization stripped out), and the site tracks both throughout.

### Key results

- **Saturation Mechanism** — the local Euler factor `1 − min(n+1,p)/p²`
  *freezes* at `1 − 1/p` once `p ≤ n+1`; each prime "saturates" the block in
  turn as `n` grows, which is the single most visually communicable idea in
  the whole project.
- **Radical Dependence** — `C(n)` (in its multi-block generalizations) depends
  on a modulus only through its radical `rad(k)` — confirmed numerically to
  high precision.
- **Mertens decomposition** — splitting the product at `n` gives
  `C(n) = ζ(2) · ∏_{p≤n}(1 − 1/p) · ∏_{p>n}(1 − (n+1)/p²)`, with asymptotic
  ratio `C(n)·ln n → ζ(2)e^(−γ)` as `n → ∞`.

Every original result on this site is checked against a self-test harness
(`selftest.html`) of known-answer tests against published constants (OEIS
`A013661`, `A065474`, `A065469`, and others), plus cross-page consistency
checks, before it's allowed to stay. Claims that didn't hold up numerically
were downgraded or cut rather than patched — two full pages were removed
outright during the project's audit for exactly this reason.

Classical foundations this project stands on — Euler, Dirichlet, Riemann,
Mertens, Farey, Ford, Ramanujan, Gauss, Cayley, and many more, each credited
against the specific pages that use their work — are listed in full in the
in-app **Credits** panel (top nav, on `index.html`). C(n) itself, its
multi-block generalizations `C(n₁,…,n_k)`, and the character-twisted `C_χ(n)`
are original constructions; the credits panel exists precisely to keep that
boundary clear.

---

## The index page (`index.html`)

`index.html` is the hero/opener page — a single, fullscreen-capable canvas
with five interchangeable lattice views of `C(n)`:

| View | What it shows |
|---|---|
| **Grid** | Raw `(r, M)` residue lattice |
| **Ring** | Concentric modular rings, one per `M` |
| **Farey** | Residues plotted by their reduced fraction `r/M` |
| **Gauss** | Gaussian-integer lattice, `a+bi` |
| **Cayley** | Conformal map `Γ(z) = (z−1)/(z+1)` (an RF Smith chart, repurposed as pure lattice geometry) |

Around the canvas:

- **Lift Dynamics** — a prime-spiral overlay (`r → r mod(M+1)`), mirror
  symmetry σ, and a `±n` path tracer, layered on top of any of the five views.
- **Goldbach overlay** — live even-number decompositions plotted directly on
  the lattice.
- **Asymptotic / Finite Π toggle** — switch the live formula between the true
  infinite product and a truncated partial product at a chosen `p_k`, with
  every dependent number (C(n), D(n), block/saturation stats) updating together.
- **Export pipeline** — 2K/4K/8K PNG export (true powers of two), plus a
  multi-view composite export for side-by-side comparisons.
- **Canvas-only fullscreen** — the whole control stack (view picker, mode
  toggle, formula, D(n), Show Working, selected points, sector path, gap
  diagonal, active gaps, Goldbach, advanced ring/character filter) relocates
  into the fullscreened canvas so nothing is left stranded off-screen.
- **Send to Hero** — carries the opener's current view/state onto the
  page's own hero section for a clean export shot.

---

## The other 14 pages

Each page is a standalone deep-dive; all fifteen (plus this opener) share the
same navigation bar, typography (Cinzel / Spectral / JetBrains Mono), and
gold/teal/coral color language. Short version of what's on each — the full
version lives in the **Page Info** dropdown at the top of `index.html`:

| Page | Title | What's most interesting |
|---|---|---|
| **P2** | How C(n) Works — Guided Walkthrough | Builds the formula piece by piece into a full live working table, nothing hidden |
| **P3** | Color & Label Modes — The Mathematics | 34 color/label modes, each a function of `(r, M, n)`, driven from one sticky master control bar |
| **P4** | The Prime Filter — Sieve View | Watches the literal Eratosthenes sieve run prime by prime on a fixed block |
| **P5** | Gap Diagonal Identity | Diagonal gaps between block-coprime residues as `n` grows |
| **P6** | Strip Correlations — Where Independence Breaks | The exact correlation factor that forces `min(n+1, p)` into the formula |
| **P7** | `C(n₁,n₂)` — Multi-Block Density / Prime Gaps | Twin/cousin/sexy-prime presets; at `n=0` the correlation ratio becomes the exact finite picture behind prime gaps |
| **P8** | `C(n₁,…,n_k)` — k-Block Density / Prime Constellations | Full k-fold generalization, with a 3D Ring view stacked by block-1 depth |
| **P9** | Dirichlet Character-Twisted Density | `C(n)` twisted by a character `χ mod Q`, linked live to its `L(s,χ)` Euler product |
| **P10** | Farey & Unit Circle | Ten representations of the unit circle; a spectral-correlation panel against GUE / Poisson / actual ζ zeros |
| **P11** | Farey Sequence Summatory Function | Exact / Hybrid / Formula toggle — brute-force enumeration vs. closed-form, side by side |
| **P12** | The Prime Spiral | Isolates the Lift Dynamics spiral for one fixed prime across every ring modulus |
| **P13** | Gauss Circle ↔ Farey Sector Bridge | `N(R) = 1 + 4A + 4D + 8O` lattice-point decomposition, in 2D and 3D |
| **P14** | `ζ(½ + it)` — Critical-Line Spiral | Root-finds ζ zeros live via Riemann–Siegel `Z(t)`, not from a stored list |
| **P15** | Sector-Graded Farey Discrepancy | Grades the Franel–Landau sum (RH-equivalent growth rate) by sector — a fraction's sector index turns out to be its first continued-fraction partial quotient |

*(P1 is `index.html` itself, described above.)*

---

## Tech

Single-file-per-page static HTML/CSS/JS — no build step, no framework.
MathJax for typeset formulas, Canvas 2D for every lattice render. Open any
page directly in a browser, or serve the folder with any static file server.

```bash
python3 -m http.server 8000
# then open http://localhost:8000/index.html
```

## Status / verification

- `selftest.html` — known-answer tests against published OEIS constants,
  plus cross-page consistency checks.
- Every page's ⌘-style **Status** button exports a full state report
  (parameters, theoretical vs. measured values, canvas snapshots) to PDF.

## License / attribution

C(n), its generalizations, and the block-coprimality framing are original
work by Wessen Getachew. Classical results this project builds on and
measures against are fully credited, page by page, in the in-app Credits
panel and referenced inline throughout.

---

*Enjoying this project? Support for new equipment is welcome via the PayPal /
BTC links on `index.html`.*


---

## Site map

| Page | What it is |
|---|---|
| **1 — Main Explorer** | Six synchronized lattice views (Grid, Ring, Farey, Lift, Gauss, Cayley), live Euler-product calculator, and connections to Goldbach's conjecture, π(x), and prime gaps |
| **2 — Gap Diagonal Identity** | Proves the lattice's diagonal strips have exact coprime density φ(g)/g, extended to block-coprimality |
| **3 — Color & Label Codex** | Reference documentation for every color/label mode used across the site, with live swatches |
| **4 — How C(n) Works** | A guided, plain-language derivation of the formula, piece by piece |
| **5 — Strip Correlations** | Works out exactly how the diagonal strips of Page 2 fail to be independent — and why that's the same mechanism behind C(n)'s two-regime kernel |
| **6 — Farey Summatory Function** | A companion research platform applying Mertens' summatory totient formula to Farey sector intervals, with harmonic/audio and Stern–Brocot tooling |
| **7 — Farey & Unit Circle** | Modular residue rings as a discrete lens on the unit circle, plus Franel–Landau/RH exploration and spectral statistics |
| **8 — The Prime Spiral** | A single fixed prime's residue traced across rings of growing modulus — explicitly *not* the Ulam spiral — plus an exponential-sum "interferometer" |
| **9 — C(n₁,n₂)** | Two independent blocks at once; doubles as an elementary twin/cousin/sexy-prime density calculator |
| **10 — C(n₁,…,n_k)** | The k-block generalization, connected to prime constellations, brute-force verified |
| **11 — The Prime Filter** | An *exact*, finite sieve for one specific block anchor M, contrasted with the M-averaged asymptotic density used everywhere else |
| **12 — C_χ(n)** | Dirichlet-character-twisted density, replacing ζ(2) with a genuine L-function value L(2,χ) |
| **13 — The Prime Spiral (standalone)** | A cleaner, focused version of Page 8's spiral construction |

---

## What's original here

**C(n)** itself, its generalizations **C(n₁,…,n_k)** and **C_χ(n)**, the block-coprimality framing, the
lift-dynamics visualization, and the prime-spiral construction are original work. They build on — and are
carefully distinguished from — classical results: Euler's product for ζ(2), the Feller–Tornier constant,
Farey sequences, Ford circles, Stern–Brocot trees, Hardy–Littlewood's singular series, and the
Franel–Landau equivalence to the Riemann Hypothesis. Each page cites its classical foundations directly.

---

## Tech

- Static, single-file HTML/CSS/JS per page — no build step, no dependencies to install
- Canvas 2D for every lattice/ring/spiral rendering
- MathJax for formula rendering
- Runs entirely client-side; open any page directly in a browser

### Running locally

```bash
git clone <repo-url>
cd <repo-name>
# just open index.html (or any pageN.html) directly in a browser
```

No server required, though some browsers restrict local file access for certain features (exports,
audio) — a simple local server avoids that:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Author

Wessen Getachew — 2026

If this project is useful to you, a ⭐ on the repo is appreciated.
