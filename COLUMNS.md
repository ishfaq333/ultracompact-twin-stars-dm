# Column definitions

## `grids/<combo>/two_fluid_full.dat`

Whitespace-separated, `#`-prefixed header lines carry the transition parameters of the
normal-matter EoS. 26 columns, one row per grid point `(p^c_NM, p^c_DM)`.

| # | name | unit | meaning |
|---|------|------|---------|
| 1 | Pc_DM | MeV/fm^3 | central DM pressure (slice label) |
| 2 | ec_NM | MeV/fm^3 | central NM energy density |
| 3 | ec_DM | MeV/fm^3 | central DM energy density |
| 4 | Pc_NM | MeV/fm^3 | central NM pressure |
| 5 | Pc_DM | MeV/fm^3 | central DM pressure |
| 6 | M | M_sun | total gravitational mass |
| 7 | M_NM | M_sun | NM gravitational mass |
| 8 | M_DM | M_sun | DM gravitational mass |
| 9 | R_total | km | R_grav = max(R_NM, R_DM) |
| 10 | R_NM | km | NM (visible) radius |
| 11 | R_DM | km | DM radius |
| 12 | f_DM | - | M_DM / M_tot |
| 13 | Compactness | - | M_tot / R_grav |
| 14 | z_total | - | surface redshift at R_grav |
| 15 | z_NM_surf | - | surface redshift at R_NM, vacuum formula (see README) |
| 16 | k2 | - | l=2 tidal Love number |
| 17 | Lambda | - | dimensionless tidal deformability |
| 18 | A_NM | - | NM surface area factor |
| 19 | A_DM | - | DM surface area factor |
| 20 | N_NM | - | conserved NM particle number |
| 21 | N_DM | - | conserved DM particle number |
| 22 | dM_dNB | - | dM / dN_B |
| 23 | detJ | - | determinant of the 2x2 particle-number Jacobian |
| 24 | stable_hippert | +1/-1 | dM/dN_B > 0 |
| 25 | stable_jac | +1/-1 | detJ > 0, the two-fluid stability criterion |
| 26 | phase | 0/1 | 0 = hadronic core, 1 = quark core |

Stability: use column 25 (`stable_jac`). The single-fluid turning point dM/dp^c > 0 is
not the stability boundary for two gravitationally coupled fluids.

## `grids/<combo>/z_metric_grid.npz`

NumPy archive, arrays aligned row-for-row with `two_fluid_full.dat`.

| key | meaning |
|-----|---------|
| `pc_nm`, `pc_dm` | central pressures, MeV/fm^3 |
| `z_nm` | surface redshift at R_NM, vacuum formula (identical to column 15) |
| `z_met` | surface redshift at R_NM, Phi-integrated (see README) |
| `z_tot` | surface redshift at R_grav |
| `M`, `R_nm`, `R_dm`, `f_dm`, `C` | as above |
| `stable` | two-fluid stability flag |
