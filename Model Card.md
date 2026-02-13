**1. Overview**

**Approach name:** Sequential Bayesian Optimisation

**Approach type:** Model-based black-box optimisation strategy

**Version:** v1.0

This approach is a sequential, data-efficient optimisation strategy designed for black-box functions where gradients and internal structure are unavailable. The model iteratively proposes inputs, observes scalar outputs, updates an internal surrogate model, and balances exploration and exploitation.

**2. Intended Use:**

This approach is intended for black-box optimisation with expensive or limited evaluations in low- to moderate-dimensional (2D–8D) continuous input spaces where the objective function is unknown, and is not suitable for high-dimensional problems (over 10 dimensions) under tight budgets, scenarios requiring guaranteed global optimality, or settings where evaluations are cheap enough to allow exhaustive search.

**3. Approach Details:**

In the initial phase, the model fits a probabilistic surrogate to observed data and uses an acquisition function (e.g., expected improvement or UCB) to balance exploration of uncertain regions with exploitation of high-performing areas, updating the surrogate after each evaluation. In the refinement phase, it shifts focus toward local search around promising regions, progressively reducing exploration to maximize the best-observed performance within the evaluation budget.

**4. Performance Summary:**

The model is evaluated on the maximization of eight black-box benchmark functions, and performance is measured relative to the maximum value achieved within the allotted outputs. Overall, the approach demonstrates satisfactory improvements across all functions, with particularly strong performance on Function 5, achieving over 500% improvement.

**5. Assumptions and Limitations:**

The approach assumes that the objective function is reasonably smooth, inputs are continuous and bounded, and observations remain stationary across rounds. Limitations include degraded performance in higher dimensions, sensitivity to surrogate model misspecification, potential local optima introduced during acquisition optimisation, and limited robustness to sharp discontinuities or chaotic objectives.

**6. Ethical Considerations and Transparency:**

The approach promotes transparency and reproducibility through explicit documentation of the sampling strategy, surrogate model assumptions, and acquisition logic, enabling consistent replication across benchmarks and implementations and supporting fair comparison with alternative optimisation methods employed by other researchers.
