# UV continuation audit — 2026-10-21

This note links the ultraviolet reconstruction repository to the [published MQGT-SCF source checkpoint](https://github.com/Cbaird26/mqgt-scf-continued/tree/62e61bf71d991e17f9110b887e4a8dc194b7075a). The report and complete offline package are prepared; GitHub release publication and asset uploads remain pending. The [planned release (pending)](https://github.com/Cbaird26/mqgt-scf-continued/releases/tag/v2026.10.21-research-continuation) will contain the report, complete offline inputs, new calculation scripts, numerical records, and source hashes.

**Audited source:** [`0a644a41eb947509280cbd648996d98bad54bdc5`](https://github.com/Cbaird26/uv-reconstruction-frg/tree/0a644a41eb947509280cbd648996d98bad54bdc5). Findings below apply to that pinned revision. This publication adds a documentation follow-up; it does not modify this repository's upstream solver or represent these corrections as already integrated into it.

## Result and scope

The formal 33-coordinate spectrum is reproduced with eight positive, twelve zero, and thirteen negative critical exponents under `theta = -eig(d beta / d coupling)`. The pinned upstream test suite passed all 44 tests. These checks establish the tested numerical identities. They do not establish a complete coupled physical ultraviolet fixed point or its critical-surface dimension.

The continuation adds a scalar-potential projection through field degree six, a six-scalar gravity-block sensitivity calculation, nonlinear matter-subsystem probes, and a convention audit. The complete-flow acceptance flag remains **false**.

## Corrections and bounded new results

| Item | Finding | Scope |
|---|---|---|
| Cosmological coordinate | The DEP branch implements `lambdaN = 2 Lambda_tilde`; `-4.7975095169` and `-2.3987547585` describe the same point in those coordinates. | Coordinate conversion, with unchanged eigenvalues under the corresponding regular transformation. |
| Sector labels | The three mass-squared exponents are `+2`; the three nonminimal-coupling exponents are approximately `+2.855435254`. The pinned prose interchanges these labels. | Corrects labels without changing the formal sign count. |
| Scalar feedback | A single six-scalar LPA trace produces sextic-to-quartic feedback absent from the assembled quartic module. | New scalar-only projection with regular normalized kinetic terms. |
| Finite differences | The largest original sextic-exponent deviation from its canonical value is `0.0027939677`. Polynomial projection recovers `-2` at the stated Gaussian matter point. | Removes a numerical differentiation artifact. |
| Scalar census | Changing the DEP block from four to six real scalars changes `gN*` from `1.7621271177` to `1.9858609514`, and `Lambda_tilde*` from `-2.3987547585` to `-2.6261976695`. | Conditional gravity-block sensitivity, without a complete mixed-sector recomputation. |
| Nonlinear marginal sector | The tested matter-only gauge subsystem and positive self-quartic rays run despite zero linearized exponents. | Does not resolve the complete gravity-coupled center manifold. |

For the documented potential normalization—mass terms divided by two, quartic monomials by four, and sextic monomials by eight—the scalar-only trace is

\[
\partial_t U=\frac{1}{32\pi^2}\operatorname{tr}(I+U^{(2)})^{-1}.
\]

At zero mass and quartic couplings, its new feedback coefficients include

\[
\frac{\partial\beta_{\lambda_H}}{\partial c_{H6}}
=-\frac{24}{32\pi^2}=-0.07599088773,
\qquad
\frac{\partial\beta_{\lambda_\Phi}}{\partial c_{\Phi6}}
=\frac{\partial\beta_{\lambda_E}}{\partial c_{E6}}
=-\frac{15}{32\pi^2}=-0.04749430483.
\]

The calculation uses a finite matrix-resolvent expansion to obtain the Taylor coefficients through degree six. It neither supplies graviton–matter mixed projections nor silently changes the reproduction of the pinned assembled flow.

Two additional normalization issues are documented in the full audit. The Narain–Percacci potential convention requires `lambda2 = m^2/2` at canonical kinetic normalization, while the pinned wiring uses `lambda2 = m^2`. In the separate Litim wrapper, restoring the paper's Newton coordinate requires `G k^2 = (24 pi) g_equation`; the equation-level fixed point `1/64` therefore restores to `3 pi/8`. That wrapper is not called by the reproduced DEP calculation. The underlying conventions are given in [Narain–Percacci, equations (1), (25), and (26)](https://arxiv.org/abs/0911.0386), [Litim, equations (5), (6), and (11)](https://arxiv.org/abs/hep-th/0606044), and the [DEP gravity–matter calculation](https://arxiv.org/abs/1311.2898).

## Requirements for a common physical flow

Completion still requires one compatible background, regulator, gauge, field count, and operator basis; regular kinetic or essential-coupling coordinates; every retained beta-function projection; coupled nonlinear analysis; and infrared matching. Eight declared coefficients remain unavailable at the reported point: `a_R2`, `a_C2`, `c_HBox`, `c_PhiBox`, `c_EBox`, `c_HF2`, `c_PhiF2`, and `c_EF2`.

The low-energy common action in the wider continuation also permits a broader simultaneous-Z2 scalar tensor and an off-diagonal Higgs portal. Its mapping into the UV source's separately even singlet basis must be demonstrated or the UV basis extended. A change of field names alone does not provide that matching.

## Reproduce and inspect

Publication of the full offline ZIP is pending. Once it is available from the [planned release (pending)](https://github.com/Cbaird26/mqgt-scf-continued/releases/tag/v2026.10.21-research-continuation), extract it and run the following command inside its `uv/` directory:

```bash
python continue_uv.py
```

The optional `--reference-difference` argument reruns the slower upstream nested finite-difference comparison. The ordinary command recomputes the new calculations and uses the recorded comparison only when its pinned source revision matches.

The detailed evidence is in `uv/UV_CONTINUATION_NOTE.md`, `uv/results.json`, `uv/projection_contract.json`, and `uv/provenance.json`. Source files, calculation assumptions, and interpretation boundaries are retained in the bundle. Verification here is internal computational checking, not independent experimental confirmation or external peer review.
