# ESL: pp 16-20

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

=> **Conditioning on $X$**: $EPE(f)=E_XE_Y([Y-f(X)]^2|X)$

=> solution (*regression* function): $f(x)=E(Y|X=x)$



K-nearest neighbor:

- expectation is approximated by averaging over sample data

- conditioning at a point is relaxed to conditioning on some region

  “close” to the target point.

- The rate of convergene decreases as the dimension *k* increases.



k-nn and least squares end up approximating conditional expectations by averages. But, the assumptions are different

- Least squares: *f(x)* is well approximate by a globally linear function
- k-nn: *f(x)* is well approximated by a locally constant function.



如果把 EPE(f) 里的 L2 loss 换成 L1 loss 即 $EPE(f)=E_XE_Y(|Y-f(X)|\ |X)$. 则实际上，解得的是

$\hat{f}(x)=\mbox{median}(Y|X=x)$.




