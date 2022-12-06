---
title: "Strang Decomposition A=CR"
excerpt_separator: "<!--more-->"
categories:
  - Mathematics
tags:
  - Post Formats
  - readability
  - standard
---
**discovered by Gilbert Strang**

Matrix decompositions are interesting and important because we are able to represent complicated things as combination of simple things. Strang decompostion, $$ A = CR $$, expresses any matrix $$A$$ as a product of a matrix that describes its Column space $$C$$ and a matrix that describes its Row space $$R$$.
 
There are various types of matrix decomposition, including lower-upper decomposition $$A=LU$$, eigenvalue decomposition $$A = X\Lambda X^{-1}$$, singular value decomposition $$A = U\Sigma V^{T}$$, and QR decomposition $$A=QR$$. They all share the same structure, which is that the complicated matrix on the left is represented as the result of either simple matrices or matrices with a high degree of structure. Among all the decomposition we have, the simplest to compute is the strang decomposition.
### Example
Given a matrix $$A$$:

$$ A = \begin{bmatrix}
1 & 3 & 5 & 15 & 0 & 2\\
2 & 6 & 4 & 24 & 0 & 1\\
4 & 12 & 1 & 41 & 0 & 1
\end{bmatrix}$$

#### Solution
First, we solve for matrix $$ R $$ through reduced row echelon form. The first is at $$A_{11}$$ where $$A_{21}$$ and $$A_{31}$$ need to be zero. This is done as follows:
 * Multiply row $$ 1 $$ by $$ 2 $$ and subtract it row $$ 2 $$ then replace the row $$ 2 $$ with the answer.
 * Multiply row $$ 1 $$ by $$ 4 $$ and subtract it row $$ 3 $$ then replace the row $$ 3 $$ with the answer.

It gives

$$ A = \begin{bmatrix}
1 & 3 & 5 & 15 & 0 & 2\\
0 & 0 & 6 & 6 & 0 & 3\\
0 & 0 & 19 & 19 & 0 & 7
\end{bmatrix}$$

Simplify row $$ 2 $$ by divinding by $$ 6 $$:

$$ A = \begin{bmatrix}
1 & 3 & 5 & 15 & 0 & 2\\
0 & 0 & 1 & 1 & 0 & \frac{1}{2}\\
0 & 0 & 19 & 19 & 0 & 7
\end{bmatrix}$$

Now our pivot is $$ A_{23} $$. We need $$ A_{13} $$ and $$ A_{33} $$ need to be zero. This is done as follows:
 * Multiply row $$ 2 $$ by $$ 5 $$ and subtract it row $$ 1 $$ then replace the row $$ 1 $$ with the answer.
 * Multiply row $$ 2 $$ by $$ 19 $$ and subtract it row $$ 3 $$ then replace the row $$ 3 $$ with the answer.

It gives

$$ A = \begin{bmatrix}
1 & 3 & 0 & 10 & 0 & \frac{1}{2}\\
0 & 0 & 1 & 1 & 0 & \frac{1}{2}\\
0 & 0 & 0 & 0 & 0 & \frac{3}{2}
\end{bmatrix}$$

Remove the fraction in the last row by multiplying by $$ \frac{2}{3} $$:

$$ A = \begin{bmatrix}
1 & 3 & 0 & 10 & 0 & \frac{1}{2}\\
0 & 0 & 1 & 1 & 0 & \frac{1}{2}\\
0 & 0 & 0 & 0 & 0 & 1
\end{bmatrix}$$

Now our pivot is $$ A_{36} $$. We need $$ A_{16} $$ and $$ A_{26} $$ need to be zero. This is done as follows:
 * Multiply row $$ 3 $$ by $$ \frac{1}{2} $$ and subtract it row $$ 1 $$ then replace the row $$ 1 $$ with the answer.
 * Multiply row $$ 3 $$ by $$ \frac{1}{2} $$ and subtract it row $$ 2 $$ then replace the row $$ 2 $$ with the answer.

It gives

$$ R = \begin{bmatrix}
1 & 3 & 0 & 10 & 0 & 0\\
0 & 0 & 1 & 1 & 0 & 0\\
0 & 0 & 0 & 0 & 0 & 1
\end{bmatrix}$$

The pivots are in column $$ 1, 3 and 6 $$. Thus, C is the pivot of the original matrix $$ A $$


$$\begin{bmatrix}
1 & 3 & 5 & 15 & 0 & 2\\
2 & 6 & 4 & 24 & 0 & 1\\
4 & 12 & 1 & 41 & 0 & 1
\end{bmatrix} = \begin{bmatrix}
1 & 5 & 2 \\
2 & 4 & 1\\
4 & 1 & 1 
\end{bmatrix} \begin{bmatrix}
1 & 3 & 0 & 10 & 0 & 0\\
0 & 0 & 1 & 1 & 0 & 0\\
0 & 0 & 0 & 0 & 0 & 1
\end{bmatrix}$$

### Code - Matlab

```ruby
function [C,R] = cr(A)
    % [C,R] = cr(A) is Strang's column-row factorization, A = C*R.
    % If A is m-by-n with rank r, then C is m-by-r and R is r-by-n.
    % Numerically reliable only when elements of A are ratios of small integers.
      [R,j] = rref(A);
      r = length(j);     % r = rank.
      R = R(1:r,:);      % R(:,j) == eye(r).
      C = A(:,j);
end
```

Thank you.

