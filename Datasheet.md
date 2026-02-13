**1. Motivation**

This dataset was created to support research and experimentation in black-box optimisation and sequential decision-making problems. The functions and example scenarios are designed to mimic real-world optimisation tasks where the internal structure of the objective function is unknown or expensive to evaluate.

**2. Composition**

The dataset comprises eight synthetic optimisation functions (Function 1 to Function 8), each defined by a function identifier, input dimensionality ranging from 2D to 8D, multi-dimensional array inputs, scalar (1D) outputs, and a maximisation objective, along with natural-language descriptions of example application contexts. There are no gaps or missing values in the dataset. 

**3. Collection Process**

The data were collected through an iterative, weekly Bayesian optimisation procedure. At each iteration, a probabilistic surrogate model based on a Gaussian Process was trained on all observations accumulated up to that point. The subsequent evaluation point for each function was determined by optimising an acquisition criterion. Following submission of the selected query points, the corresponding true function values were returned in the next cycle. These newly obtained evaluations were appended to the dataset, after which the surrogate model was retrained to reflect the expanded evidence base. This sequential update–selection process was carried out once per week, resulting in a progressively enriched dataset and increasingly informed search behaviour.

**4. Preprocessing and Uses**

During the initial phase of data collection, no normalization or scaling procedures were applied to the recorded outputs. However, as optimisation progressed and substantial increases in objective values were observed, the magnitude of the outputs began to affect the stability of the Gaussian Process surrogate model.
To address this, output normalization was introduced in subsequent iterations to ensure numerically stable kernel estimation and more reliable hyperparameter optimisation within the surrogate model. This preprocessing step improved model conditioning and supported more robust acquisition-driven query selection.

**5. Distribution and Maintenance**

The dataset is maintained within the repository’s designated data folder on GitHub and is updated as new query point results become available; its use is intended to be restricted to internal, educational, or research purposes and not for commercial applications.
