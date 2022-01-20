# ESL: pp 41 - 50

## Linear Methods for Regression

Linear regression model:

- $f(X)=\beta_0+\sum_{j=1}^pX_j\beta_j$

Minimize residual sum of squares

$RSS(\beta)=\sum_{i=1}^N(y_i-f(x_i))^2=\sum_{i=1}^N(y_i-\beta_0-\sum_{j=1}^px_{ij}\beta_j)^2$.

Matrix form:

$RSS(\beta)=(\textbf{y}-\textbf{X}\beta)^T(\textbf{y}-\textbf{X}\beta)$.

Differentiating with $\beta$:

=> $\frac{\partial RSS}{\partial \beta}=-2\textbf{X}^T(\textbf{y}-\textbf{X}\beta)$.

=> $\frac{\partial^2\ RSS}{\partial \beta\ \partial\beta^T}=2\textbf{X}^T\textbf{X}$.



#### Case 1:

If $\textbf{X}$ full column rank, $\textbf{X}^T\textbf{X}$ positive definite

=> $\textbf{X}^T(\textbf{y}-\textbf{X}\beta)=0$ => $\hat{\beta}=(\textbf{X}^T\textbf{X})^{-1}\textbf{X}^T\textbf{y}$.



Projected values $\hat{f}(x_0)=(1:x_0)^T\hat{\beta}$ at input vector $x_0$.

- Matrix from:
  - $\hat{\textbf{y}}=\textbf{X}\hat{\beta}=\textbf{X}(\textbf{X}^T\textbf{X})^{-1}\textbf{X}^T\textbf{y}$
  - $\textbf{H}=\textbf{X}(\textbf{X}^T\textbf{X})^{-1}\textbf{X}^T$ => *projection* matrix



#### Case 2:

If the columns $\textbf{X}$ are not linearly indepedent,  $\textbf{X}^T\textbf{X}$ is singular.

More than one way to express the *projection*.

Typical solution: recode or drop redundant columns in $\textbf{X}$.



Form test of hypothesis and confidence intervals for the parameters $\beta_j$:

TODO



z-score: measure the effect of droppping the variable from the model.

