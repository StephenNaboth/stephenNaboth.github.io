---
title: "Singular Value Decomposition"
excerpt_separator: "<!--more-->"
categories:
  - Mathematics
tags:
  - Post Formats
  - readability
  - standard
---

# **Singular Value Decompostion application to Image Compression**

The singular value decomposition (SVD) is an important matrix factorization technique that provides a numerically stable matrix
decomposition that can be used for a variety of purposes such as to obtain low-rank approximations to matrices and to perform pseudo-inverses of non-square matrices to find the solution of a system
of equations $$\text{Ax = b}$$.

Generally, we are interested in analyzing a large data set $$X \in \mathbb{C}^{n\times m}$$.

$$
\mathbf{X}=\left[\begin{array}{cccc}
\mid & \mid & & \mid \\
\mathbf{x}_1 & \mathbf{x}_2 & \cdots & \mathbf{x}_m \\
\mid & \mid & & \mid
\end{array}\right]
$$

For many systems $$ n \gg m $$, resulting in a tall-skinny matrix, as opposed to a short-fat matrix when $$ n \ll m $$. 
The SVD is a unique matrix decomposition that exists for every complex valued
matrix $$ X \in \mathbb{C}^{n\times m} $$:

$$
\mathrm{X} = \mathrm{U\Sigma V}^*
$$

where $$ U \in \mathbb{C}^{n\times n} $$ and $$ V \in \mathbb{C}^{m\times m} $$ are **unitary matrices** with orthonormal columns, and $$ \mathrm{\Sigma} \in \mathbb{C}^{n\times m} $$ is a matrix with real, non-negative entries on the diagonal and
zeros off the diagonal.

When $$ n \geq m $$, the matrix $$ \mathrm{\Sigma} $$ has at most m non-zero elements on the diagonal, and may be written as

$$
\boldsymbol{\Sigma}=\left[\begin{array}{l}
\hat{\Sigma} \\
0
\end{array}\right] \text {. }
$$

Therefore, it is possible to exactly represent X using the economy SVD:

$$
\mathrm{X} = \mathrm{U\Sigma V}^* = \left[\begin{array}{ll}
\hat{U} & \hat{U}^{\perp}
\end{array}\right]\left[\begin{array}{c}
\hat{\Sigma} \\
0
\end{array}\right] \mathrm{V}^* = \hat{U}\hat{\Sigma}\hat{V}^*
$$

The columns of $$ \hat{U}^{\perp} $$ span
a vector space that is complementary and orthogonal to that spanned by $$ \hat{U} $$.
The columns of V are **right singular vectors** and the columns of U are called **left singular vectors** of X. The diagonal elements of $$\hat{\Sigma} \in \mathbb{C}^{n\times m}$$ are called **singular values** and they are ordered from largest to smallest. The rank of X is equal to the number of non-zero singular values.
In order to find $$ U, \Sigma \text{ and } V$$ we use:

$$
\mathrm{X}^* \mathrm{X}=\mathrm{V}\left[\begin{array}{ll}
\hat{\Sigma} & 0
\end{array}\right] \mathrm{U}^* \mathrm{U}\left[\begin{array}{c}
\hat{\Sigma} \\
0
\end{array}\right] \mathrm{V}^*=\mathrm{V} \hat{\Sigma}^2 \mathrm{~V}^*
$$
and

$$
XV = U\Sigma
$$



### Example

Find the singular value decomposition of the matrix:

$$
A = \begin{bmatrix}
1 & 3\\
2 & 6
\end{bmatrix}
$$

$$
\mathrm{A}^T \mathrm{A}=\mathrm{V}\left[\begin{array}{ll}
\hat{\Sigma} & 0
\end{array}\right] \mathrm{U}^T \mathrm{U}\left[\begin{array}{c}
\hat{\Sigma} \\
0
\end{array}\right] \mathrm{V}^*=\mathrm{V} \hat{\Sigma}^2 \mathrm{~V}^T
$$
and

$$
AV = U\Sigma
$$

$$
\mathrm{A}^T \mathrm{A} = \begin{bmatrix}
1 & 3\\
2 & 6
\end{bmatrix} \begin{bmatrix}
1 & 2\\
3 & 6
\end{bmatrix} = \begin{bmatrix}
5 & 15\\
15 & 45
\end{bmatrix} 
$$


### Application

#### Image Compression through matrix approximation

The most useful and defining property of the SVD is that it provides an optimal low-rank approximation to a matrix $$X$$. Thus, high-dimensional data may be well described by a few dominant
patterns given by the columns of $$ \hat{U} \text{ and } \hat{V}$$.
We consder the image of a bridge at the beach as shown below This image has size of $$2000 \text{ by } 1125$$ pixels.

**Original**
![Original](/assets/images/svd/landscape_3.jpg)

**Gray**
![Grey](/assets/images/svd/grey.png)

<!-- <img src="/assets/images/svd/landscape_3.jpg" alt="landscape" style="width:400px;"/>| ![landscape_gray](/assets/images/svd/grey.png) -->

We apply the svd code on this image:

- The code is provided below
- run the svd.py
- The plots below show truncation of the columns to when $$ r = 5, 10, 20 \text{ and } 50 $$

![Results](/assets/images/svd/results_r.png)

<!-- r =5                          |    r =10                         | r=20
:----------------------------:|:--------------------------------:|:-------------------:
![r_5](/images/img_5.png)|![r_10](/images/img_10.png)  | ![r_20](/images/img_20.png)  -->

Plot the diagonal singular values:

-     Run the scd_analysis.py code
  The result

![Analysis](/assets/images/svd/analysis.png)

<!-- Singular values                     |    Cummulatve Singular Values
:----------------------------------:|:----------------------------------------:
![singular values](/images/singular_values_plot_1.png) | ![singular values](/images/singular_values_plot.png) -->

Test for around 92% of the cummulative energy where r = 400. we get:

![r_400](/assets/images/svd/test_r_400.png)

The above steps can be done in the matlab file. Just by running SVD_1.m

.That's all. Thank You
