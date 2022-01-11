# ESL: pp 1-15

## Ch2: Overview of Supervised Learning

Supervised learning:

- Goal: use the inputs to predict values of the outputs



Inputs: predictors, independent variables, features

Outputs: responses, dependent variables



#### Variable types

1. Quantitative variables: some measurements are bigger than others, and measurements close in value are close in nature

2. Qualitative variables: categorical, discrete variables, factors



Prediction tasks based on the output type:

- Regression: when we predict quantitative outputs
- Classification: when we predict qualitative outputs



3. Ordered categorical: small, medium, large. There is an ordering between the values, but no metric notion is appropriate 



Learning task:

- Given the value of an input vector $X$, make a good prediction of the output $Y$, denoted by $\hat{Y}$. If $Y$ takes values in $\mathbb{R}$, then so should $\hat{Y}$. likewise for categorical outputs, $\hat{G}$ should take values in the same set $\mathcal{G}$ associated with $G$.



### Least Squares and Nearest Neighbors

#### Linear Models and Least Squares

Given a vector of inputs $X^T=(X_1,X_2,\cdots,X_p)$, we predict the output $Y$ via the model $\hat{Y}=\hat{\beta}_0+\sum_{j=1}^pX_j\hat{\beta}_j$.

=> Include $\hat{\beta}_0$ in vector $\hat{\beta}$: $\hat{Y}=X^T\hat{\beta}$.

Fit the linear model to a set of training data using **least squares**

pick the coefficients $\beta$ to minimize the residual sum of squares 

- $$RSS(\beta)=\sum_{i=1}^{N}(y_i-x_i^T\beta)^2$$

- matrix form: $$RSS(\beta)=(\textbf{y}-\textbf{X}\beta)^T(\textbf{y}-\textbf{X}\beta)$$

- Differentiating w.r.t. $\beta$ => *normal equations* $$\textbf{X}^T(\textbf{y}-\textbf{X}\beta) = 0$$.

- If $\textbf{X}^T\textbf{X}$ is nonsingular, the unique solution: $\hat{\beta}=(\textbf{X}^T\textbf{X})^{-1}\textbf{X}^Ty$.

 The entire fitted surface is characterized by the *p* parameters $\beta$



#### Nearest Neighbor Methods

Use those observations in the training set $\mathcal{T}$ Closet in input space to $x$ to form $\hat{Y}$.

We find the *k* observations with $x_i$ closest to $x$ in input space, and average their responses.

The *k*-nearest neighbor fit for $\hat{Y}$ is defined as follows:

- $$\hat{Y}(x)=\frac{1}{k}\sum_{x_i\in N_k(x)}y_i$$.

Effective number of parameters of $k$-nearest neighbors is $N/k$ and is generally bigger than $p$, and decreases with increasing $k$.

