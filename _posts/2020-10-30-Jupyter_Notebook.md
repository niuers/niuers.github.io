---
title: "Jupyter Notebook"
date: 2020-10-30
categories:
  - blog
tags:
  - bit
  - programming
---

<div class="cell markdown">

#### Problem VII.1.1

For the original function, \(F=ReLU(x)+ReLU(y)+ReLU(z)\), we have 8
linear pieces, i.e.

1.  \(F = x+y+z\), where \(x>0,y>0,z>0\)

<!-- end list -->

  - \(F=x+y\), where \(x>0,y>0,z<0\)
  - \(F=x+z\), where \(x>0,y<0,z>0\)
  - \(F=x\), where \(x>0,y<0,z<0\)
  - \(F=y+z\), where \(x<0,y>0,z>0\)
  - \(F=y\), where \(x<0,y>0,z<0\)
  - \(F=z\), where \(x<0,y<0,z>0\)
  - \(F=0\), where \(x<0,y<0,z<0\)

If we add the \(4\)th fold of \(ReLU(x+y+z)\), its fold plane is
\(x+y+z=0\), for this fold plane to cut the original pieces, it requires
solution for the fold plane in each piece. It's clear to see that no
solution exists for the first (\(x>0,y>0,z>0\)) and last piece
(\(x<0,y<0,z<0\)). The new fold plane doesn't cut through them. So there
are a total of \(2\times 6 + 2 = 14\) pieces.

The \(14\) pieces are:

1.  \(F = 2x+2y+2z\), where \(x>0,y>0,z>0\)

<!-- end list -->

  - \(F=2x+2y+z\), where \(x>0,y>0,z<0, x+y+z > 0\)
  - \(F=x+y\), where \(x>0,y>0,z<0, x+y+z < 0\)
  - \(F=2x+y+2z\), where \(x>0,y<0,z>0, x+y+z > 0\)
  - \(F=x+z\), where \(x>0,y<0,z>0, x+y+z < 0\)
  - \(F=2x+y+z\), where \(x>0,y<0,z<0, x+y+z > 0\)
  - \(F=x\), where \(x>0,y<0,z<0, x+y+z < 0\)
  - \(F=x+2y+2z\), where \(x<0,y>0,z>0, x+y+z > 0\)
  - \(F=y+z\), where \(x<0,y>0,z>0, x+y+z < 0\)
  - \(F=x+2y+z\), where \(x<0,y>0,z<0, x+y+z > 0\)
  - \(F=y\), where \(x<0,y>0,z<0, x+y+z < 0\)
  - \(F=x+y+2z\), where \(x<0,y<0,z>0, x+y+z > 0\)
  - \(F=z\), where \(x<0,y<0,z>0, x+y+z < 0\)
  - \(F=0\), where \(x<0,y<0,z<0\)

#### Problem VII.1.2

\(r(N,2) = N(N,0)+N(N,1)+N(N,2) = 1 + N + \frac{N(N-1)}{2} = \frac{1}{2}N^2 + \frac{N}{2} + 1\)

It has a leading term \(\frac{1}{2}N^2\)

#### Problem VII.1.3

If \(N=18\) and we have 9 vertical and 9 horizontal lines, in total we
have \((9+1)\times (9+1) = 100\) pieces of the plane.

On the other hand \(r(18,2) = N(18,2) + N(18,1) + N(18,0) = 172\) which
is a lot more than with parallel lines.

#### Problem VII.1.4

We have \(A_1=\begin{bmatrix} 1 & 2 \\ 3 & -1 \\ 2 & 5 \end{bmatrix}\),
and \(b_1=\begin{bmatrix} -4 \\ 1 \\ -6 \end{bmatrix}\), so we have
\(A_1v_0+b_1 = \begin{bmatrix} 1 & 2 \\ 3 & -1 \\ 2 & 5 \end{bmatrix}\begin{bmatrix}x \\ y \end{bmatrix} +\begin{bmatrix} -4 \\ 1 \\ -6 \end{bmatrix}\).

If the output \(w\)is the sum of those three ReLU's, we have \(N=3\) and
\(m=2\), so \(r(3,2) = 3 + 3 + 1 = 7\) pieces in \(w(x,y)\).

#### Problem VII.1.5

According to formula (4), we have
\(r(4,3) = N(4,3)+N(4,2)+N(4,1)+N(4,0) = 4 + 6 + 4 + 1 = 15\). Folding
\(R^3\) four times we have 15 flat subsets.

#### Problem VII.1.6

For \(a=b=1\), we have \(2^N = \sum^N_{k=0} {N \choose k} = r(N,N)\).
The coefficients \(N \choose k\) sum up to \(2^N\)

If we fold \(R^N\) space \(N\) times, we have \(2^N\) pieces. For
\(r(N,m)\) with \(m\ge N\), we always get \(2^N\) pieces.

#### Problem VII.1.7

After five folds, we have \(r(5,2) = r(4,2) + r(4,1) = 11 + 5 = 16\)

#### Problem VII.1.8

  - Choose the maximum among two linear functions create a piecewise
    linear function. If the original functions are continuous, the
    maximum of them is also continuous.

  - The sum of two CPL is also CPL. We are always adding two linear
    functions.

  - For each \(x\), we first apply a linear transformation using
    \(F_1\), then we apply a second linear function \(F_2\), the
    composition stays linear.

#### Problem VII.1.9

If \(m=4\) and \(N=6\) with 3 hidden layers.

  - The first hidden layer, weight matrix is 6 by 4, and bias is 6 by 1,
    so we have total 30 parameters.
  - The second hidden layer, weight matrix is 6 by 6, and bias is 6 by
    1, so we have total 42 parameters.
  - The third hidden layer, weight matrix is 6 by 6, and bias is 6 by 1,
    so we have total 42 parameters.
  - The output layer, weight matrix is 1 by 6, no bias, so we have 6
    parameters.

In total we have \(30+42+42+6 = 120\) parameters.

There are 6 ReLU functions in each total, with a total of 18 ReLU
functions in the network.

#### Problem VII.1.10

If we play with the example 2 at <http://playground.tensorflow.org/>, we
can see that with 2 hidden layers:

  - 8 + 2: is much easier to find the solution, takes much less epochs
    to separate all the points.
  - 2 + 8: usually takes much longer to find a solution, and the
    solution can't completely separate all the points.

So we should put more of neurons in layer 1 instead of layer 2.

</div>

<div class="cell markdown">

#### Problem VII.1.11

  - The learning succeed for \(N=4\), the count \(r(4,2)= 11\). There
    are 6 sides in the polygon.

#### Problem VII.1.12

Reduce \(N=3\), \(F\) still classfies blue and orange correctly. There
are \(r(3,2) = 7\) flat pieces. There are 4 sides in the separating
polygon.

#### Problem VII.1.13

Reduce \(N=2\), \(F\) doesn't classify the blue and orange correctly.
The count \(r(2,2) = 4\). There are 4 folds in the graph of \(F(v)\).

There are 3 sides in the white separator, note the white separator is
not closed.

#### Problem VII.1.14

If we apply on example 2 on playground.tensorflow.org, we see that
\(N=3\) classifies the training data correctly, it doesn't work when
\(N=2\).

Guess we need at least 5 flat pieces to successfully classify the
points.

When \(N=2\), we have \(F(v)\) split into 3 regions, top right we have
\(F(v)=1\), top left we have \(F(v)=-1\), and the bottom, we have
\(F(v)=0\)

#### Problem VII.1.15

For example 4, as we increase \(N\), the whole data is split into two
parts for \(N=1\), and the split increases, until about 4-5 splits when
\(N=8\). However, with just 1 layer, and maximum 8 neurons on the
website, it's impossible to classify the example 4 data points
successfully.

#### Problem VII.1.16

  - \(4+4\) doesn't seem to classify the points
  - \(6+2\) doesn't seem to classify the points
  - \(2+6\) doesn't seem to classify the points

I can't tell that \(6+2\) is better or worse than \(2+6\) from the
graph. However, the loss on test data is smaller with \(6+2\) than
\(2+6\).

#### Problem VII.1.17

For 2 hidden layers, I tried 7 by 8 that seems to be able to separate
the points completely.

With 3 hidden layers, it's pretty easy to separate the points with 5 by
5 by 4 network.

#### Problem VII.1.18

The smallest number of pieces that 20 fold lines can produce in a plane
should be 2 when all of the lines overlap with each other.

#### Problem VII.1.19

For 10 vertical and 10 horizontal folds, we have \(11\times 11 = 121\)
pieces

#### Problem VII.1.20

The maximum number of pieces from 20 fold lines should be
\(r(20,2) = 211\)

</div>

<div class="cell markdown">

#### Problem VII.2.1

We obtain the 5 by 5 discrete Gaussian \(G\) from wikipedia on [Kernel
(image
processing)](https://en.wikipedia.org/wiki/Kernel_\(image_processing\))
using Gaussian blur \(5\times 5\). We have the Gaussian matrix from wiki
as

\(G=\frac{1}{256}\begin{bmatrix}1 & 4 & 6 & 4 & 1 \\ 4 & 16 & 24 & 16 & 4 \\ 6 & 24 & 36 & 24 & 6 \\ 6 & 24 & 36 & 24 & 6 \\ 4 & 16 & 24 & 16 & 4 \\ 1 & 4 & 6 & 4 & 1 \end{bmatrix}\).

It's easy to check that
\(G=\frac{1}{256} \begin{bmatrix} 1 \\ 4 \\ 6 \\ 4 \\ 1 \end{bmatrix} \begin{bmatrix} 1 & 4 & 6 & 4 & 1\end{bmatrix}\)

See below for the different effects of this filter and the book's filter
(equation 3) on a horizontal edge and a diagonal edge.

It looks like that both Gaussian matrices have similar effects on the
edges, i.e. smooth (blur) the original edge. The Gaussian matrix from
equation (3) displays sharper edges after filtering than the wikipedia
Gaussian.

</div>

<div class="cell code" data-execution_count="44">

``` python
#### Problem VII.2.1

import numpy as np

# Discrete Gaussian from wikipedia
gau_wiki = np.array([[1, 4, 6, 4, 1], [4, 16, 24, 16, 4], [6, 24, 36, 24, 6], [4, 16, 24, 16, 4], [1, 4, 6, 4, 1]])
print('Gaussian matrix from wikipedia  (before normalization): \n', gau_wiki)

u1 = np.array([[1, 4, 6, 4, 1]]).reshape(-1, 1)
v1 = u1.transpose()

#u, s, vh = np.linalg.svd(gau_wiki, full_matrices=True)
#u.shape, s.shape, vh.shape
print('Gaussian 5 by 5 equals to its rank-1 approximation: ', np.allclose(np.matmul(u1, v1)/256, gau_wiki/256))


# Discrete Gaussian from equation (3)

gau = np.array([[1, 4, 7, 4, 1], [4, 16, 26, 16, 4], [7, 26, 41, 26, 7], [4, 16, 26, 16, 4], [1, 4, 7, 4, 1]])
print('Gaussian matrix from equation 3 (before normalization): \n', gau)

ones = np.ones((1,5))
zeros = np.zeros((1,5))
horizontal_edge = np.vstack([ones, ones, ones, zeros, zeros])
print('Horizontal edge: \n', horizontal_edge)

ones = np.ones((5,5))
diagonal_edge = np.tril(ones)
print('Diagonal edge: \n', diagonal_edge)

#gau_wiki = gau_wiki/256
#gau = gau/273

# Apply on Horizontal Edge
gh_wiki = np.matmul(gau_wiki, horizontal_edge)
gh = np.matmul(gau, horizontal_edge)
print("\n---------------------- Output -------------------\n")
print("Note: To see better the effect of filtering, we don't normalize the Gaussian matrices here")
print('Apply Wiki Gaussian to Horizontal Edge: \n', gh_wiki)
print('Apply Equation 3 Gaussian to Horizontal Edge: \n', gh)

# Apply on Diagonal Edge
gd_wiki = np.matmul(gau_wiki, diagonal_edge)
gd = np.matmul(gau, diagonal_edge)

print('Apply Wiki Gaussian to Diagonal Edge: \n', gd_wiki)
print('Apply Equation 3 Gaussian to Diagonal Edge: \n', gd)
```

<div class="output stream stdout">

    Gaussian matrix from wikipedia  (before normalization): 
     [[ 1  4  6  4  1]
     [ 4 16 24 16  4]
     [ 6 24 36 24  6]
     [ 4 16 24 16  4]
     [ 1  4  6  4  1]]
    Gaussian 5 by 5 equals to its rank-1 approximation:  True
    Gaussian matrix from equation 3 (before normalization): 
     [[ 1  4  7  4  1]
     [ 4 16 26 16  4]
     [ 7 26 41 26  7]
     [ 4 16 26 16  4]
     [ 1  4  7  4  1]]
    Horizontal edge: 
     [[1. 1. 1. 1. 1.]
     [1. 1. 1. 1. 1.]
     [1. 1. 1. 1. 1.]
     [0. 0. 0. 0. 0.]
     [0. 0. 0. 0. 0.]]
    Diagonal edge: 
     [[1. 0. 0. 0. 0.]
     [1. 1. 0. 0. 0.]
     [1. 1. 1. 0. 0.]
     [1. 1. 1. 1. 0.]
     [1. 1. 1. 1. 1.]]
    
    ---------------------- Output -------------------
    
    Note: To see better the effect of filtering, we don't normalize the Gaussian matrices here
    Apply Wiki Gaussian to Horizontal Edge: 
     [[11. 11. 11. 11. 11.]
     [44. 44. 44. 44. 44.]
     [66. 66. 66. 66. 66.]
     [44. 44. 44. 44. 44.]
     [11. 11. 11. 11. 11.]]
    Apply Equation 3 Gaussian to Horizontal Edge: 
     [[12. 12. 12. 12. 12.]
     [46. 46. 46. 46. 46.]
     [74. 74. 74. 74. 74.]
     [46. 46. 46. 46. 46.]
     [12. 12. 12. 12. 12.]]
    Apply Wiki Gaussian to Diagonal Edge: 
     [[16. 15. 11.  5.  1.]
     [64. 60. 44. 20.  4.]
     [96. 90. 66. 30.  6.]
     [64. 60. 44. 20.  4.]
     [16. 15. 11.  5.  1.]]
    Apply Equation 3 Gaussian to Diagonal Edge: 
     [[ 17.  16.  12.   5.   1.]
     [ 66.  62.  46.  20.   4.]
     [107. 100.  74.  33.   7.]
     [ 66.  62.  46.  20.   4.]
     [ 17.  16.  12.   5.   1.]]

</div>

</div>

<div class="cell markdown">

#### Problem VII.2.2

I would use this matrix to find the gradients in the \(45^o\) diagonal
direction.

\(S=\frac{1}{2}\begin{bmatrix}-1& -1 & 0 \\ -1 & 0 & 2 \\ 0 & 2 & 2 \end{bmatrix}\)

#### Problem VII.2.3

Suppose
\(v=\begin{bmatrix}v_{11} & v_{12} & v_{13} \\v_{21} & v_{22} & v_{23} \\v_{31} & v_{32} & v_{33} \end{bmatrix}\)

So the \((1,1)\) element of \(Av\) is
\(x_{00}v_{11} + x_{-10}v_{12} + x_{0-1}v_{21} + x_{-1-1}v_{22}\)

The \((2,2)\) element of \(Av\) is
\(x_{11}v_{11} + x_{01}v_{12} + x_{-11}v_{13} + x_{10}v_{21} + x_{00}v_{22} + x_{-10}v_{23} + x_{1-1}v_{31} + x_{0-1}v_{32} + x_{-1-1}v_{33}\).

#### Problem VII.2.4

We have

  - \(L_1V = \begin{bmatrix} 0 & 4 & -4 & 0 \\ 0 & 4 & -4 & 0\end{bmatrix}\)

  - \(L_2V = \begin{bmatrix} 0 & 24 & -24 & 0 \\ 0 & 24 & -24 & 0\end{bmatrix}\)

  - \(L_1D = \begin{bmatrix} 0 & 2 & -2 & 0 \\ 2 & -2 & 0 & 0\end{bmatrix}\)

  - \(L_2D = \begin{bmatrix} 1 & 9 & -9 & -1 \\ 9 & -9 & -1 & 0\end{bmatrix}\)

#### Problem VII.2.5 TODO

#### Problem VII.2.6 TODO

#### Problem VII.2.7 TODO

</div>

<div class="cell markdown">

#### Problem VII.3.1

If \(x,y\) are in \(R^n\), then:

  - \(x(y^Tx)\): It takes \(n + n = 2n\) multiplications
  - \((xy^T)x\): It takes \(n^2+n^2 = 2n^2\) multiplications

So it's faster to multiply \(x(y^Tx)\)

#### Problem VII.3.2

  - \(A(A^TA)\): It takes \(nmn + mnn = mn^2\) multiplications
  - \((AA^T)A\): It takes \(mnm + mmn = nm^2\) multiplications

Because \(m>n\), so we have \(nm^2 > mn^2\), it's faster to use the
first way.

#### Problem VII.3.3

  - (a) Take derivative on both sides of
    \(A_{m\times n}x_{n\times 1}=b_{m\times 1}\) w.r.t. \(b_j\), we
    have:
    \(A\frac{\partial{x}}{\partial{b_j}} = \frac{\partial{b}}{\partial{b_j}}\)
    So we have
    \(A\begin{bmatrix}\frac{\partial{x_1}}{\partial{b_j}} \\ \dots \\ \frac{\partial{x_j}}{\partial{b_j}} \\ \dots \\ \frac{\partial{x_n}}{\partial{b_j}}\end{bmatrix}=\begin{bmatrix}0 \\ \dots \\ 1 \\ \dots \\ 0\end{bmatrix}\)

Suppose the \(\frac{\partial{x}}{\partial{b}}\) is the Jacobian matrix
of \(x\) w.r.t. \(b\). So we have
\(A_{m\times n}\frac{\partial{x}}{\partial{b}}_{n\times m} = I_{m\times m}\).
The entry \(\frac{\partial{x_i}}{\partial{b_j}}\) is thus solution of
the equation.

  - (b) Let's change the matrix \(A_{m\times n}\) to a 1 by \(mn\)
    vector, with
    \(A_{11},\dots, A_{1n},A_{21},\dots,A_{2n},\dots, A_{m1},\dots, A_{mn}\)
    in the entries. So the Jacobian of \(x\) w.r.t. \(A\) has
    \(n \times mn\) elements.

Take derivative of \(x\) w.r.t. \(A_{jk}\) on both sides of the equation
\(Ax=b\), we have

\\begin{align*} A\_{11}\\frac{\\partial{x\_1}}{\\partial{A\_{jk}}} +
A\_{12}\\frac{\\partial{x\_2}}{\\partial{A\_{jk}}} + \\dots +
A\_{1n}\\frac{\\partial{x\_n}}{\\partial{A\_{jk}}} &= 0\\ \\dots \\
A\_{j1}\\frac{\\partial{x\_1}}{\\partial{A\_{jk}}} +
(A\_{jk}\\frac{\\partial{x\_k}}{\\partial{A\_{jk}}} + x\_k) + \\dots +
A\_{jn}\\frac{\\partial{x\_n}}{\\partial{A\_{jk}}} &= 0\\ \\dots \\
A\_{m1}\\frac{\\partial{x\_1}}{\\partial{A\_{jk}}} +
A\_{m2}\\frac{\\partial{x\_2}}{\\partial{A\_{jk}}} + \\dots +
A\_{mn}\\frac{\\partial{x\_n}}{\\partial{A\_{jk}}} &= 0\\ \\end{align*}

Write in matrix format we have

\(A\begin{bmatrix}\frac{\partial{x_1}}{\partial{A_{jk}}} \\ \dots \\\frac{\partial{x_k}}{\partial{A_{jk}}} \\ \dots\\ \frac{\partial{x_n}}{\partial{A_{jk}}}\end{bmatrix} + \begin{bmatrix}0 \\ \dots \\ x_k \\ \dots \\ 0 \end{bmatrix} = 0\)

Collect all terms, we have

\(A_{mn}J_{n(mn)} + X_{m(mn)}= 0\) where we have
\(X_{j, (k-1)n+1:kn} = x^T\) and zeros on all other columns on the
\(j\)th row.

For example, when \(m=2,n=3\), we have
\(X=\begin{bmatrix} x_1 & x_2 & x_3 & 0 & 0 & 0 \\ 0 & 0 & 0 & x_1 & x_2 & x_3 \end{bmatrix}\)

So the derivatives in \(J\) are the solution of this equation.

#### Problem VII.3.4

For \(x\) and \(y\) in \(R^n\), we have

  - \(x^Ty = \sum x_iy_i\): so
    \(\frac{\partial{x^Ty}}{\partial{x_i}} = y_i\)
  - For \(A=xy^T\), we have \(A_{ij} = x_iy_j\), so
    \(\frac{\partial{A_{jk}}}{\partial{x_i}} = \delta_{ji}y_k\)

#### Problem VII.3.5

It's easy to see that \(f(2,3) = -8\) through the computational graph.

#### Problem VII.3.6

Through computational graph, if we let \(s=x^3\), \(c=x-y\), then
\(F=sc\), so we have \(s=8,c=-1\)

  - \(\frac{\partial{F}}{\partial{x}} = \frac{\partial{F}}{\partial{s}}\frac{\partial{s}}{\partial{x}} + \frac{\partial{F}}{\partial{c}}\frac{\partial{c}}{\partial{x}} = c(3x^2) + s\times 1 = (-1)\times(3\times 2^2) + 8\times 1 = -4\)

  - \(\frac{\partial{F}}{\partial{y}} = \frac{\partial{F}}{\partial{s}}\frac{\partial{s}}{\partial{y}} + \frac{\partial{F}}{\partial{c}}\frac{\partial{c}}{\partial{y}} = s \times (-1) = -8\)

#### Problem VII.3.7

\(w_i = a_{1-i}v_1 + a_{2-i}v_2 + \dots + a_{i-i}v_i + \dots + a_{n-i}v_n = \sum a_{j-i}v_j\),
so we have \(\frac{\partial{w_i}}{\partial{a_k}} = v_{k+i}\)

#### Problem VII.3.8

\(\frac{\partial{w_i}}{\partial{v_j}} = \delta_{j=2i-1}\delta_{v_{2i-1}>v_{2i}}+\delta_{j=2i}\delta_{v_{2i-1}\le v_{2i}}\)

#### Problem VII.3.9

\(\frac{d\sin(\cos(\sin x))}{dx} = \frac{d\sin(\cos(\sin x))}{d\cos(\sin x)}\frac{d\cos(\sin x)}{d\sin x}\frac{d\sin x}{dx} = \cos(\cos(\sin x)) \left(-\sin(\sin x)\right) \cos x = 0\)

</div>

<div class="cell code">

``` python
```

</div>
