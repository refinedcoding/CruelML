# ESL: pp 16-30

#### From Least Squares to Nearest Neighbors

Linear decision boundary: 

- low variance, potentially high bias



k-nearest-neighbor procedure

- high variance, low bias

#### 2.4 Statistical Decision Theory

- $X\in\mathbb{R}^p$: a real valued random input vector
- $Y\in\mathbb{R}$: a real valued output variable
- Joint distribution $Pr(X,Y)$.

Seek a function $f(X)$ minimize *loss function* $L(Y,f(X))$.

- example: squared error loss: $L(T,f(X)) = (Y-f(X))^2$

=> expected (squared) prediction error: $EPE(f)=E(Y-f(X))^2=\int[y-f(x)]^2Pr(dx,dy)$.  

=> conditioning on $X$: $EPE(f)=E_XE_Y([Y-f(X)]^2|X)$

=> solution (*regression* function): $f(x=E(Y|X=x))$

K-nearest neighbor:

- expectation is approximated by averaging over sample data

- conditioning at a point is relaxed to conditioning on some region

  “close” to the target point.

TODO
