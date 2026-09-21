# Formalisation of the Invariance of Domain Theorem

A Lean 4 formalisation of the invariance of domain theorem, submitted in partial fulfilment of the MSci in Mathematics at Imperial College London, September 2026.

**Author:** Kai Lam
**Supervisor:** Steven Sivek

## The Theorem

The invariance of domain theorem states that a continuous injective map from an open subset of R^n to R^n is open.

A direct corollary is invariance of dimension: R^n and R^m are homeomorphic if and only if n = m. This is essential for classifying topological manifolds and proving that the dimension of a manifold is well-defined.

## What Is Formalised

The development comprises approximately 1500 lines of Lean 4. It compiles without errors and contains no uses of `sorry`.

### Part 1: No smooth retraction (self-contained)

`cont_diff_ball_to_sphere_no_fixed` — for a nontrivial finite-dimensional real inner product space E, there is no continuously differentiable map from the closed unit ball to the unit sphere that fixes the sphere pointwise.

This follows Rogers's simplification of Milnor's proof. It uses an integral argument: the integral of the determinant of the derivative would simultaneously be the volume of the ball (by change of variables) and zero (because the derivative is singular on the interior), giving a contradiction.

This part assumes nothing beyond Mathlib.

### Part 2: Invariance of domain

The following results assume Brouwer's fixed point theorem via the typeclass `BrouwerFixedPoint E`, since it is not yet available in Mathlib:

- `invariance_of_domain_interior` — if f is continuous and injective on the closed unit ball, then f(0) lies in the interior of f(B).
- `invariance_of_domain_open_map` — a continuous injective map defined on an open subset U ⊆ E is an open map.
- `invariance_of_domain_partial_equiv` — if f is a partial equivalence and continuous on its source, then it sends neighbourhoods to neighbourhoods of the image.
- `dim_le_of_injective_continuous` — if there is a continuous injective map from E to F, then dim E ≤ dim F.
- `invariance_of_dimension` — if E and F are homeomorphic, their dimensions are equal.

This part follows Terence Tao's exposition of a proof by Kulpa.

### Auxiliary lemmas

- `differentiable_approx_of_continuous` — polynomial approximation for continuous maps on compact sets, via Stone-Weierstrass.
- `stability_of_zero` — links zeros of approximating functions to Brouwer's fixed point theorem.
- `I_eq_volume_of_bij` — a change-of-variables formula for bijections with positive Jacobian.
- `I_eq_poly_eval` — expresses the integral of the determinant as the evaluation of a polynomial.
- `poly_const_of_const_on_Ico` — a polynomial constant on an interval is identically constant.

## Use of AI Assistance

AI assistance was used during this project, primarily as a tool for shortening proof blocks, separating out lemmas, and locating Mathlib theorems. The tool used was a chat with Claude, accessed via Imperial College London's instance at https://daisy.imperial.ac.uk. The full conversation is included in this repository as `Claude Chat.txt`.

All final code was checked with the Lean compiler and verified by the author. The AI was not used to generate mathematical arguments, and no proof was accepted without compilation.

## Build

Requires Lean 4 and Mathlib. To build:

    lake exe cache get
    lake build

## Repository Contents

- `M4RProject/Basic.lean` — the full formalisation
- `Claude Chat.txt` — the AI conversation referenced above
- `README.md` — this file

## Acknowledgements

I would like to thank my supervisor, Steven Sivek, for his enthusiasm and support for this project.

I would also like to thank the following people, who have given me help and guidance in Lean: Yaël Dillies, Bhavik Mehta, Kevin Buzzard, and Heather Macbeth.

## References

1. C. A. Rogers. A less strange version of Milnor's proof of Brouwer's fixed-point theorem. *American Mathematical Monthly*, 87:525–527, 1980.
2. J. Milnor. Analytic proofs of the 'hairy ball theorem' and the Brouwer fixed point theorem. *The American Mathematical Monthly*, 85(7):521–524, 1978.
3. T. Tao. Brouwer's fixed point and invariance of domain theorems, and Hilbert's fifth problem. Blog post, 2011.
4. W. Kulpa. Poincaré and domain invariance theorem. *Acta Universitatis Carolinae. Mathematica et Physica*, 39(1–2):127–136, 1998.
5. The Mathlib Community. The Lean Mathematical Library. *CPP '20*, 2020.