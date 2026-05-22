---
layout: page
title: Machine Learning Notes
permalink: /blog/machine_learning/
description: Notes and exercises from the EECS 545 curriculum.
---

Notes and worked out exercises based off of EECS 545 schedule posted [here](https://github.com/thejakeyboy/umich-eecs545-lectures?tab=readme-ov-file). 

# Lectures 1-3

Derivation of Sum and Product rules. Consider the following box 

$$
\begin{array}{c|c|c|c}
  & c_1 & c_2 & c_3 \\
\hline
r_1 & n_{11} & n_{12} & n_{13} \\
\hline
r_2 & n_{21} & n_{22} & n_{23} \\
\hline
r_3 & n_{31} & n_{32} & n_{33} \\
\end{array}
$$

$x_i$ is value of some random variable $X$ that can range from $i=1,..,M$, while $y_i$ is similarly the value of some random variable $Y$ that can range from $i=1,..,L$. $n_{ij}$ is the number of instances that $X=x_i,Y=y_i$ in row $r_j$ and column $c_i$, and $N$ is the total number of instances $X$ and $Y$. The joint probability of an event $P(X=x_i,Y=y_i)$ is defined as follows

$$
P(X=x_i,Y=y_i) = \frac{n_{ij}}{N}.
$$

To derive the marginal probability of a variable, begin by noting that $p(X=x_i)$ is simply the total number of points that fall into column $c_i$ so 

$$
p(X=x_i) = \sum_{j}^{L}p(X=x_i,Y=y_j).
$$

The conditional probability is defined as the probability of an instance $X=x_i$ given that $Y=y_j$ has occured, and can be interpreted as the fraction of instances in row $r_j$ that also fall under $c_i$. So

$$
p(X=x_i | Y=y_i) = \frac{n_ij}{r_j}.
$$

So the product rule is then

$$
P(X=x_i,Y=y_j) = \frac{n_{ij}}{N} = \frac{n_{ij}}{c_{j}} \frac{c_{j}}{N} = p(X=x_i | Y=y_j) p(Y=y_j).
$$

Since $p(X,Y)=p(Y,X)$ then we have that 

$$
p(X=x_i | Y=y_j) p(Y=y_j) = p(Y=y_j | X=x_i) p(X=x_i)
$$

or more compactly

$$
p(X|Y) = \frac{p(Y|X)p(X)}{p(Y)}.
$$

Finish up probability derivations.