+++
date = '2025-02-22T21:09:00+08:00'
draft = false
title = 'Derivatives of matrix functions'
categories = ['Math', 'Calculus']
tags = ['Math', 'Calculus']
katex = true
+++
The derivative of trace or determinant with respect to the matrix is vital when calculating the derivate of lagrangian in matrix optimization problems and finding the  maximum likelihood estimation of multivariate gaussian distribution.  

## Matrix-Valued Derivative

Let $f$ be a scaler function of a matrix $X \in \mathbb{R}^{n\times n}$, the derivative of it with respect to $X$ can be defined as following
$$
\left(\frac{\partial f}{\partial X}\right)_{ij} = \frac{\partial f}{\partial X\_{ij}}
$$
That is to say, the derivative is a matrix, the element of which is the derivative with respect to the element of matrix $X$. 

## Derivative of Trace

Now, let $f$ be the trace of $X$
$$
f(X) = tr(X) = \sum_{i}X_{ii}
$$
Then, it's easy to find that
$$
\frac{\partial f}{\partial X_{ii}} = 1 
$$
We can write in the matrix form
$$
\frac{\partial tr(X)}{\partial X} = I
$$
Moreover, 
$$
f(X) = tr(AXB) = \sum_{ijk}A_{ij}X_{jk}B_{ki}
$$
Then 
$$
\frac{\partial f}{\partial X_{jk}} = \sum_{i}A_{ij}B_{ki} = (BA)\_{kj} = (A^TB^T)\_{jk}
$$
So that
$$
\frac{\partial tr(AXB)}{\partial X} = A^TB^T
$$
Similarly, if $f$ be the trace of square of the matrix, then
$$
f(X) = tr(X^2) = \sum_{i}(X^2)\_{ii} = \sum_{ik}X_{ik}X_{ki} = \sum_{i}X^2_{ii} + \sum_{k>i}2X_{ik}X_{ki}
$$
 so 
$$
\frac{\partial tr(X^2)}{\partial X_{ik}} = 2X_{ki}
$$
Thus, we have
$$
\frac{\partial tr(X^2)}{\partial X} = 2X^T
$$

## Derivative of Determinant

The determinant of a matrix is complicated to expressed as the summation of its elements,  however, from the Laplace expansion, also known as cofactor expansion, we have
$$
det(X) = \sum_{j}(-1)^{i+j}X_{ij}M_{ij}
$$
so
$$
\frac{\partial det(X)}{\partial X_{ij}} = (-1)^{i+j}M_{ij} = (adj(A)^T)_{ij}
$$
where $adj(A)$ is the adjugate matrix of $A$, so
$$
\frac{\partial det(X)}{\partial X} = adj(A)^T = det(A^T)A^{-T} = det(A)A^{-T}
$$

## Maximum Likelihood Estimation

Given a data set $\{x_1, x_2, \cdots, x_n\}$ sampled from a multivariate Gaussian distribution. We want to estimate the parameters of the distribution via maximum likelihood.  

The probability density function of multivariate Gaussian distribution is
$$
f(x; \mu, \Sigma) = \frac{1}{(2\pi)^{d/2}|\Sigma|^{1/2}}e^{\frac{-(x-\mu)\Sigma^{-1}(x-\mu)^T}{2}}
$$
We form the log likelihood function by taking the logarithm of product of $n$ Gaussian distributions:
$$
l(x; \mu, \Sigma) = -\frac{nd}{2}\log{2\pi} - \frac{n}{2}\log{|\Sigma|} - \frac{1}{2}\prod_{i=1}^n(x_i-\mu)\Sigma^{-1}(x_i-\mu)^T
$$
 We need to take the derivative with respect to $\Sigma$ an set to zero.  

As previously mentioned, 
$$
\frac{\partial \log{|\Sigma|}}{\partial \Sigma^{-1}} = \frac{1}{|\Sigma|}\frac{\partial |\Sigma|}{\partial \Sigma^{-1}} = \frac{1}{|\Sigma|}\frac{\partial}{\partial \Sigma^{-1}}\frac{1}{|\Sigma^{-1}|} = -\Sigma^T
$$
and
$$
\frac{\partial x\Sigma x^T}{\partial \Sigma} = \frac{\partial tr( x\Sigma x^T)}{\partial \Sigma} = \frac{\partial tr( xx^T\Sigma)}{\partial \Sigma} = (xx^T)^T=xx^T
$$
so
$$
\frac{\partial l}{\partial \Sigma^{-1}} = \frac{n}{2}\Sigma^T - \frac{1}{2}\prod_{i=1}^n(x_i-\mu)(x_i-\mu)^T
$$
Finally, setting to zero yield the maximum likelihood estimator:
$$
\Sigma_{ML} = \frac{1}{n}\prod_{i=1}^n(x_i-\mu)(x_i-\mu)^T
$$


## Reference

- [Matrix Calculus - Notes on the Derivative of a Trace](http://paulklein.ca/newsite/teaching/matrix%20calculus.pdf)

- [Laplace expansion - Wikipedia](https://en.wikipedia.org/wiki/Laplace_expansion)
- [Adjugate matrix - Wikipedia](https://en.wikipedia.org/wiki/Adjugate_matrix)
- [The Multivariate Gaussian](https://people.eecs.berkeley.edu/~jordan/courses/260-spring10/other-readings/chapter13.pdf)

