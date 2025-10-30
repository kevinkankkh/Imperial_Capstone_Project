# Imperial_Capstone_Project
# 1.	Project overview
This project is the capstone project of the Professional Certificate in Machine Learning and Artificial Intelligence of Imperial College Business School. It mimics a Bayesian optimisation-style competition, i.e. there is a black-box function, with initial data points provided to participants who will build a statistical surrogate model of the black-box function and acquisitions function to submit multiple rounds of intelligent queries to find the optimum solutions, using Bayesian optimization technique and limited total number of queries.
Such setting mirrors real-world machine learning problem, of which the analytical expression of the underlying problem is unknown (i.e. black-box function) and cost to find such expression is costly (thereby the total number of queries is limited given the cost).
This project serves as a practice exercise for participants to apply skills and knowledge acquired in this Certificate program to real-world problems.

# 2.	Inputs and outputs
In this project, there are 8 black-box functions to optimise.
## Function 1: f: R2 ---> R 
Detect likely contamination sources in a two-dimensional area, such as a radiation field, where only proximity yields a non-zero reading
## Function 2: f: R2 ---> R 
Imagine a black box, or a mystery ML model, that takes two numbers as input and returns a log-likelihood score. The goal is to maximise that score, but each output is noisy, and depending on where you start, you might get stuck in a local optimum. 
## Function 3: f: R3 ---> R 
This is a drug discovery project, testing combinations of three compounds to create a new medicine. The inputs are the amounts of the three compounds used while the outputs are the number of adverse reactions (1D array). The goal is to minimise side effects; in this competition, it is framed as maximisation by optimising a transformed output (e.g. the negative of side effects). 
## Function 4: f: R4 ---> R 
This task addresses the challenge of optimally placing products across warehouses for a business with high online sales, where accurate calculations are costly and only feasible biweekly. To speed up decision-making, an ML model approximates these results within hours. The model has four hyperparameters to tune, and its output reflects the difference from the expensive baseline. Because the system is dynamic and full of local optima, it requires careful tuning and robust validation to find reliable, near-optimal solutions.
## Function 5: f: R4 ---> R 
This task is to optimise a four-variable black-box function that represents the yield of a chemical process in a factory. The function is typically unimodal, with a single peak where yield is maximised.  The goal is to find the optimal combination of chemical inputs that delivers the highest possible yield, using systematic exploration and optimisation methods.
## Function 6: f: R5 ---> R
This task is to optimise a cake recipe using a black-box function with five ingredient inputs, for example flour, sugar, eggs, butter and milk. Each recipe is evaluated with a combined score based on flavour, consistency, calories, waste and cost, where each factor contributes negative points as judged by an expert taster. This means the total score is negative by design. 
To frame this as a maximisation problem, the goal is to bring that score as close to zero as possible or, equivalently, to maximise the negative of the total sum.
## Function 7: f: R6 ---> R 
This task is to optimise an ML model by tuning six hyperparameters, for example learning rate, regularisation strength or number of hidden layers. The function to be maximised is the model’s performance score (such as accuracy or F1), but since the relationship between inputs and output isn’t known, it’s treated as a black-box function. 
## Function 8: f: R8 ---> R 
This task is to optimise an eight-dimensional black-box function, where each of the eight input parameters affects the output, but the internal mechanics are unknown. The objective is to find the parameter combination that maximises the function’s output, such as performance, efficiency or validation accuracy. Because the function is high-dimensional and likely complex, global optimisation is hard, so identifying strong local maxima is often a practical strategy.
For example, imagine tuning an ML model with eight hyperparameters: learning rate, batch size, number of layers, dropout rate, regularisation strength, activation function (numerically encoded), optimiser type (encoded) and initial weight range. Each input set returns a single validation accuracy score between 0 and 1. The goal is to maximise this score.

# 3.	Challenge objectives
The goal of this project is to find the maximum of these 8 black-box functions with limited total number of queries (i.e. 13) 
Major challenges and constraints of this project 
-	Given limited background information about the functions and high dimensional inputs (which make visualisation hard or even impossible), it is difficult to find the right surrogate model to approximate the unknown functions
-	With limited number of queries, a balance between exploitation and exploration has to be stricken when deciding next query point 
-	The high dimensionality of certain functions would mean 
# 4.	Technical approach
Across the first three query submissions, I used Gaussian Process as the surrogate model. For functions with low dimension inputs (e.g. 2D and 3D), I created scatter plots to visualize data distribution and trend so as to determine the appropriate kernels used in surrogate model. Major kernels used included Matern, RBF and White Noise. Parameters like lengthscale and nu are tuned based on functions descriptions and scatter plot observations. 
To query the next point, I used grid search for low dimension cases and Bayesian Optimisation for high dimension cases due to the high computational costs of grid search in high dimension cases.
Moreover, using Upper Confidence Bound (UCB) and Bayesian Optimisation to find next point in high dimension case is prone to picking boundary points as random points are concentrated near high boundary points, I applied a factor to kappa in classic UCB equation to scale down the impact of high uncertainty at boundary points which leads to the tendency of picking boundary points.  
For functions with good results, I limited the search functions I limit the search location by creating a hypercube to search spaces near best performing inputs while the strategy to acquire next point focuses on exploration for functions with unsatisfactory results. 
