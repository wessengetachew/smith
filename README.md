# C(n) — Block-Coprime Density

**Live page 1 The Index.html:** https://wessengetachew.github.io/smith/

# C(n) — Block-Coprime Density

**An interactive exploration of an original analytic number theory construction, across 13 pages.**

🔗 **Live site:** [link here]

---

## The question

Pick a random integer. How likely is it to share no common factor with a fixed modulus? That's the
classical coprimality density, 6/π² ≈ 0.6079.

Now ask a harder version: how likely is it to share no common factor with a fixed modulus *and every
integer right after it, n of them in a row*? That's **C(n)** — a single Euler product that tracks this
shrinking density for every block length n, built entirely out of primes:

```
C(n) = ζ(2) · ∏ₚ (1 − min(n+1, p) / p²)
```

rescaled so that C(0) = 1 exactly. Everything on this site is built from that one formula — proved,
visualized six different ways, generalized in three directions, and worked out prime by prime.

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
