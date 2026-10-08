# Ultra-compact twin stars with hybrid EoS from bosonic dark matter — data release

Data behind **I. A. Rather, S. L. Pitz and J. Schaffner-Bielich,
"Ultra-compact twin stars with hybrid equations of state from bosonic dark matter",
[arXiv:2609.03964](https://arxiv.org/abs/2609.03964)**.

Compact stars with a strong first-order phase transition to quark matter and a second
fluid of self-interacting bosonic dark matter, solved with the two-fluid TOV equations.
Each run is a 30 x 80 grid in the central pressures `(p^c_NM, p^c_DM)`.

## Layout

```
grids/      53 parameter combinations
  <combo>/two_fluid_full.dat    master table, 26 columns
  <combo>/z_metric_grid.npz     surface redshift, both definitions
COLUMNS.md  full column definitions
```

Combination names are `P<Pt>_E<deps>_<cs2>__mb<m_b>_n<n>`:

| field | meaning | values |
|---|---|---|
| `Pt` | transition pressure, MeV/fm^3 | 10, 30, 100, 120 |
| `deps` | energy-density jump, MeV/fm^3 | 250, 400, 500, 600 |
| `cs2` | quark speed of sound squared | `10` = 1.0, `07` = 0.7 |
| `m_b` | boson mass, MeV | 100, 200, 300, 1000 |
| `n` | self-interaction exponent | 4, 40 |

Two runs carry a `_hiDM` suffix: extended central-DM-pressure range, not used in the paper.

Everything in the paper derives from `two_fluid_full.dat`. Mass-radius, tidal, stability
and redshift tables that appeared in the working tree are subsets of it and are not
duplicated here.

## Equations of state

The underlying normal-matter and dark-matter EoS tables are **not** included in this
release; what is released are the two-fluid stellar models built from them.

**Dark matter** — self-interacting bosonic dark matter with a modified scalar potential,
the boson mass `m_b` and self-interaction exponent `n` being the free parameters. Defined in:

- S. L. Pitz and J. Schaffner-Bielich, *Generating ultracompact boson stars with modified
  scalar potentials*, Phys. Rev. D **108**, 103043 (2023),
  [arXiv:2308.01254](https://arxiv.org/abs/2308.01254),
  [doi:10.1103/PhysRevD.108.103043](https://doi.org/10.1103/PhysRevD.108.103043)
- S. L. Pitz and J. Schaffner-Bielich, *Generating ultracompact neutron stars with bosonic
  dark matter*, Phys. Rev. D **111**, 043050 (2025),
  [arXiv:2408.13157](https://arxiv.org/abs/2408.13157),
  [doi:10.1103/PhysRevD.111.043050](https://doi.org/10.1103/PhysRevD.111.043050)

building on the self-interacting boson star of M. Colpi, S. L. Shapiro and I. Wasserman,
Phys. Rev. Lett. **57**, 2485 (1986),
[doi:10.1103/PhysRevLett.57.2485](https://doi.org/10.1103/PhysRevLett.57.2485).

**Normal matter** — a piecewise polytrope matched to a constant-speed-of-sound quark phase
at the transition pressure `P_t` with an energy-density jump `deps`, following
A. Kurkela, E. S. Fraga, J. Schaffner-Bielich and A. Vuorinen, Astrophys. J. **789**, 127
(2014), [arXiv:1402.6618](https://arxiv.org/abs/1402.6618),
[doi:10.1088/0004-637X/789/2/127](https://doi.org/10.1088/0004-637X/789/2/127).

The EoS tables are available from the authors on request.

## Which combinations the paper shows

| figure | combination |
|---|---|
| Fig. 1 | `P10_E250_10__mb300_n40`, `P30_E250_10__mb300_n40`, `P100_E500_10__mb300_n40`, `P120_E600_10__mb300_n40` |
| Fig. 2 | `P30_E250_10__mb1000_n4`, `P120_E400_10__mb1000_n4` |
| Fig. 3 | `P30_E250_10__mb300_n40`, `P120_E400_10__mb300_n40` |
| Fig. 4 | `P10_E250_10__mb300_n40` (two configurations) |
| Fig. 5 | `P10_E250_10__mb300_n40`, `P120_E400_10__mb300_n40`, `P10_E250_10__mb1000_n4`, `P120_E400_10__mb1000_n4` |
| Fig. 6 | `P10_E250_10__mb300_n40`, `P30_E250_10__mb300_n40` |
| Fig. 7, 8 | `P10_E250_10__mb300_n40`, `P10_E250_10__mb300_n4` |
| Appendix | `P30_E250_07__mb300_n40` |
| "ultimate twins" (text) | `P10_E250_10__mb100_n40` |

The remaining combinations are part of the same survey and are released for completeness.

## Surface redshift — which column to use

Two definitions are provided, and they are **not** interchangeable.

**`z_NM_surf`** (column 15 of `two_fluid_full.dat`, and `z_nm` in the `.npz`)

```
z_surf = [1 - 2 M(r <= R_NM) / R_NM]^(-1/2) - 1
```

counts only the mass enclosed by the normal-matter surface. **These are the values plotted
in Figs. 7 and 8 of the paper.** They are reproduced here unchanged so that the release
matches the published figures.

**`z_met`** (in the `.npz` only)

```
z_met = exp(-Phi(R_NM)) - 1,    Phi(R_grav) = (1/2) ln(1 - 2 M_tot / R_grav)
```

with `Phi` integrated inward from `R_grav` through the dark-matter distribution.

The vacuum expression above is valid only where the exterior of `R_NM` is empty. For a
**dark-matter core** (`R_DM < R_NM`) that holds, and the two agree to machine precision —
verified across all 51 grids carrying an `.npz`. For a **dark-matter halo**
(`R_DM > R_NM`) the region above the emitting surface is not vacuum, the vacuum formula
does not apply, and `z_met` is the redshift a distant observer measures.

The difference is large. For `P10_E250_10__mb300_n40`, over stable configurations:

| class | `z_nm` | `z_met` |
|---|---|---|
| DM core | 0.002 – 0.808 | 0.002 – 0.808 |
| DM halo | 0.017 – 0.771 | 0.051 – 3.468 |

**Recommendation: use `z_nm` only to reproduce the published figures. For any new analysis
of halo configurations, use `z_met`.** The discussion of the halo redshift range in the
paper follows `z_nm` and is superseded by `z_met` for those configurations.

## Stability

Use `stable_jac` (column 25), the sign of the 2x2 particle-number Jacobian determinant.
The single-fluid turning point `dM/dp^c > 0` is not the stability boundary for two
gravitationally coupled fluids; `stable_hippert` (column 24, `dM/dN_B > 0`) is provided
for comparison.

Comparing the two criteria over this grid, the branch termination moves by up to
+0.31 M_sun (two-fluid more restrictive) and down to -0.45 M_sun (less restrictive) for
`m_b` = 300–1000 MeV. For `m_b` = 100 MeV, where the dark matter forms a very extended
halo, the spread is far larger and the two criteria are not comparable in any simple way.

## Loading

```python
import numpy as np

a = np.genfromtxt("grids/P10_E250_10__mb300_n40/two_fluid_full.dat", comments="#")
M, R_NM, f_DM, Lam = a[:, 5], a[:, 9], a[:, 11], a[:, 16]
stable = a[:, 24] > 0                      # two-fluid criterion

z = np.load("grids/P10_E250_10__mb300_n40/z_metric_grid.npz")
z_observable = z["z_met"]                  # aligned row-for-row with the table above
```

## Citation

If you use this data, please cite the paper (see `CITATION.cff`).

## License

[CC BY 4.0](LICENSE).
