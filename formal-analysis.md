# The Beginning

## A Multi-AI Framework for Independent Scientific Cross-Checking

## Abstract

This project investigates whether multiple artificial intelligence systems can be used as independent analytical agents for scientific problem solving.

Instead of allowing the systems to communicate from the beginning, each AI receives the same scientific problem and performs its analysis independently.

The individual results are recorded before any comparison takes place.

Only after this blind phase are the analyses compared.

The comparison focuses on:

- mathematical agreement and disagreement,
- differences in physical interpretation,
- calculation or reasoning errors,
- assumptions introduced by individual systems,
- and the robustness of conclusions under independent cross-checking.

The purpose of the framework is not to assume that agreement between AI systems establishes scientific truth.

Multiple systems may reproduce the same error or share similar assumptions.

Instead, disagreement is treated as useful information: contradictions can identify parts of an analysis that require additional calculation, data, or human examination.

The first experimental application uses galaxy rotation-curve data and tests a simple phenomenological acceleration relation.

---

# 1. Research Objective

The central physical question is whether the relation

$$
a_{\rm model}=a_N+p\sqrt{a_Na_0}
$$

can describe galaxy rotation data in a stable and reproducible way.

The parameter \(p\) is dimensionless and must be estimated from observational data.

The fixed acceleration scale used in the initial test is

$$
a_0=1.2\times10^{-10}\ {\rm m\,s^{-2}}.
$$

A second methodological question is whether independent AI-assisted analyses, compared only after an initial blind phase, can expose hidden assumptions, calculation errors, or methodological dependence more clearly than a single analysis path.

The project follows the principle:

**Independent analysis → comparison → contradiction detection → verification**

---

# 2. Mathematical Model

## 2.1 Base Relation

The initial test relation is

$$
a_{\rm model}=a_N+p\sqrt{a_Na_0}.
$$

Here,

$$
a_N=\frac{GM}{r^2}
$$

represents the Newtonian acceleration associated with the baryonic mass distribution, while the observed centripetal acceleration is

$$
a_{\rm obs}=\frac{v^2}{r}.
$$

The model adds a square-root acceleration contribution controlled by the dimensionless parameter \(p\).

The relation is treated here as a phenomenological test model.

No physical mechanism is assumed by the fit itself.

---

# 3. Low-Acceleration Limit

Consider the regime

$$
a_N\ll a_0.
$$

If the square-root contribution dominates, then

$$
a_{\rm model}\approx p\sqrt{a_Na_0}.
$$

Using

$$
a_N=\frac{GM}{r^2}
$$

and

$$
a_{\rm model}=\frac{v^2}{r},
$$

we obtain

$$
\frac{v^2}{r}
=
p\sqrt{\frac{GM}{r^2}a_0}.
$$

For \(r>0\),

$$
v^2=p\sqrt{GMa_0}.
$$

Squaring both sides gives

$$
v^4=p^2GMa_0.
$$

Therefore the explicit dependence on radius disappears in this asymptotic limit.

For constant \(p\) and \(a_0\), the relation predicts

$$
v^4\propto M.
$$

This produces two directly testable consequences:

1. an asymptotically radius-independent rotational velocity,
2. a fourth-power velocity-mass relation.

Agreement with these mathematical consequences alone does not identify the physical origin of the relation.

It only provides observable predictions that can be tested.

---

# 4. Dataset

The empirical test uses galaxy rotation-curve data from the SPARC mass-model dataset.

The analysis file is:

`MassModels_Lelli2016c.mrt`

SHA-256 checksum:

`9108994b12cc401b94a1768beca61c53ec354779385c9c9cc571049f3043244c`

The working dataset contains:

- **175 galaxies**
- **3,391 radial measurement points**

The analysis uses fixed stellar mass-to-light factors:

$$
\Upsilon_{\rm disk}=0.5
$$

and

$$
\Upsilon_{\rm bul}=0.7.
$$

---

# 5. Baryonic Velocity Contribution

For every radial measurement point, the baryonic squared velocity contribution is calculated as

$$
V_{\rm bar}^2
=
V_{\rm gas}|V_{\rm gas}|
+
0.5V_{\rm disk}^2
+
0.7V_{\rm bul}^2.
$$

The signed gas contribution is retained because negative gas terms can occur in the source mass decomposition.

A measurement point is used only if

$$
R>0,
$$

$$
V_{\rm obs}>0,
$$

$$
eV_{\rm obs}>0,
$$

and

$$
V_{\rm bar}^2>0.
$$

Two points fail these requirements:

- UGC01281, \(R=0.08\ {\rm kpc}\)
- UGC01281, \(R=0.23\ {\rm kpc}\)

Both have a non-positive calculated baryonic squared velocity contribution.

Therefore:

- Total measurement points: **3,391**
- Excluded measurement points: **2**
- Measurement points used: **3,389**

No fitted value of \(p\) was inserted into the dataset before the analysis.

---

# 6. Unit Conversion

The radius is converted from kiloparsecs to metres using

$$
1\ {\rm kpc}
=
3.085677581491367\times10^{19}\ {\rm m}.
$$

Therefore

$$
r
=
R_{\rm kpc}
\times
3.085677581491367\times10^{19}.
$$

Velocities are converted using

$$
1\ {\rm km\,s^{-1}}
=
1000\ {\rm m\,s^{-1}}.
$$

---

# 7. Observed and Baryonic Accelerations

For each accepted measurement point, the observed centripetal acceleration is

$$
a_{\rm obs}
=
\frac{V_{\rm obs}^2}{r}.
$$

The baryonic Newtonian acceleration inferred from the rotation decomposition is

$$
a_N
=
\frac{V_{\rm bar}^2}{r},
$$

after conversion to SI units.

If \(V_{\rm bar}^2\) is expressed in \(({\rm km\,s^{-1}})^2\),

$$
a_N
=
\frac{V_{\rm bar}^2\times10^6}{r}.
$$

Define

$$
X=\sqrt{a_Na_0}
$$

and

$$
Y=a_{\rm obs}-a_N.
$$

The acceleration relation then becomes

$$
Y=pX.
$$

This allows the acceleration-space fits to be expressed as a one-parameter regression through the origin.

---

# 8. Fitting Procedure A — Unweighted Acceleration Fit

The first fit minimizes

$$
\sum_i
\left(
a_{{\rm obs},i}
-
a_{N,i}
-
p\sqrt{a_{N,i}a_0}
\right)^2.
$$

Using \(X_i\) and \(Y_i\), this becomes

$$
\sum_i(Y_i-pX_i)^2.
$$

The analytical least-squares solution is

$$
p
=
\frac{\sum_iX_iY_i}
{\sum_iX_i^2}.
$$

For all 3,389 accepted measurement points, the resulting global value is

$$
\boxed{p=0.609056}.
$$

Rounded to three decimal places:

$$
p=0.609.
$$

---

# 9. Fitting Procedure B — Error-Weighted Acceleration Fit

The propagated random acceleration uncertainty is approximated as

$$
\sigma_a
=
\frac{2V_{\rm obs}eV_{\rm obs}}{r}.
$$

Each point receives the weight

$$
w_i=\frac{1}{\sigma_{a,i}^2}.
$$

The fitted value minimizes

$$
\chi_a^2
=
\sum_i
\frac{
\left[
a_{{\rm obs},i}
-a_{N,i}
-p\sqrt{a_{N,i}a_0}
\right]^2
}
{\sigma_{a,i}^2}.
$$

The corresponding analytical estimate is

$$
p
=
\frac{\sum_iw_iX_iY_i}
{\sum_iw_iX_i^2}.
$$

The resulting global value is

$$
\boxed{p=0.714440}.
$$

Rounded to three decimal places:

$$
p=0.714.
$$

---

# 10. Fitting Procedure C — Velocity-Space Fit

The model acceleration is

$$
a_{\rm model}
=
a_N+p\sqrt{a_Na_0}.
$$

This is converted into a predicted rotational velocity using

$$
V_{\rm model}
=
\sqrt{a_{\rm model}r}.
$$

Therefore

$$
V_{\rm model}
=
\sqrt{
\left(
a_N+p\sqrt{a_Na_0}
\right)r
}.
$$

The velocity-space fit minimizes

$$
\chi_V^2
=
\sum_i
\left(
\frac{
V_{{\rm obs},i}-V_{{\rm model},i}
}
{eV_{{\rm obs},i}}
\right)^2.
$$

The resulting global value is

$$
\boxed{p=0.775356}.
$$

Rounded to three decimal places:

$$
p=0.775.
$$

---

# 11. Comparison of Global Fits

The three fitting procedures give:

| Method | Global \(p\) |
|---|---:|
| Unweighted acceleration fit | 0.609056 |
| Error-weighted acceleration fit | 0.714440 |
| Velocity-space fit | 0.775356 |

The fitted value of \(p\) therefore depends substantially on the fitting procedure.

This dependence must not be hidden.

The current results do not establish that \(p\) is a universal physical constant.

Instead, the disagreement between fitting procedures is itself an important empirical result.

---

# 12. Single-Galaxy Check — NGC 3198

NGC 3198 contains 43 radial measurement points in the working dataset.

The three fitting procedures give:

| Method | \(p\) |
|---|---:|
| Unweighted acceleration fit | 0.308858 |
| Error-weighted acceleration fit | 0.718926 |
| Velocity-space fit | 0.721081 |

The earlier value near \(p\approx0.309\) is reproduced only by the explicitly unweighted acceleration-space calculation.

Error weighting changes the estimate substantially.

This demonstrates why the fitting definition must always be stated together with the reported value of \(p\).

A successful fit to a single galaxy is not sufficient evidence for a universal relation.

---

# 13. Galaxy-to-Galaxy Variation

A separate value \(p_i\) can also be estimated for each galaxy.

## 13.1 Error-Weighted Acceleration Fits

Across the 175 galaxies:

- Mean: **0.716901**
- Median: **0.691237**
- Standard deviation: **0.425822**
- 16th percentile: **0.330033**
- 84th percentile: **1.099653**
- Minimum: **-0.403274**
- Maximum: **2.119043**

The large spread indicates that the individual galaxies are not described by one sharply concentrated value of \(p\) under the present assumptions.

## 13.2 Velocity-Space Fits

Across the individual galaxy fits:

- Mean: **0.749822**
- Median: **0.705143**
- Standard deviation: **0.425288**
- 16th percentile: **0.343328**
- 84th percentile: **1.134929**
- Minimum: **-0.281250**
- Maximum: **2.130411**

The galaxy-to-galaxy spread remains substantial.

---

# 14. Model Comparison

Within the error-weighted acceleration framework, three models were compared:

1. baryonic model with \(p=0\),
2. one global fitted value of \(p\),
3. one independent \(p_i\) for each galaxy.

The results are:

| Model | \(\
