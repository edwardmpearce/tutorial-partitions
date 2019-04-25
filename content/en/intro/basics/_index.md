+++
title = "Basics"
date =  2019-04-15T17:03:32+01:00
weight = 5
+++

> In number theory and combinatorics, a partition of a positive integer $n$, also called an integer partition, is a way of writing $n$ as a sum of positive integers. - [Wikipedia](https://en.wikipedia.org/wiki/Partition_(number_theory))

As addition is commutative, the order of the summands is arbitrary and may be rearranged so that they appear in decreasing order. For example, we may partition the integer $5$ in the following seven distinct ways:

- $5$
- $4 + 1$
- $3 + 2$
- $3 + 1 + 1$
- $2 + 2 + 1$
- $2 + 1 + 1 + 1$
- $1 + 1 + 1 + 1 + 1$

With this in mind, we begin with the following definitions: 

## First Definitions

A **partition** is a finite nonincreasing sequence of positive integers, often denoted by symbols such as $\lambda$, $\mu$, or $p$. 

In other words, if $\lambda$ is a partition, then it can be viewed as a function $\lambda:\mathbb{Z}\_{>0}\to\mathbb{Z}\_{>0}$ such that $\lambda(i)\ge\lambda(j)$ for all $i\le j$, and there is some $M\in\mathbb{Z}\_{>0}$ such that $\lambda(i)=0$ for all $i\ge M$.

We may express the data stored in a partition by writing out the finite sequence as $\lambda=(\lambda\_{1},\lambda\_{2},\ldots,\lambda\_{k})$ with $\lambda\_{1}\ge\lambda\_{2}\ge\ldots\ge\lambda\_{k}>0$. These $\lambda\_{i}$ are called the **parts** of the partition $\lambda$.

We define the **size** of a partition $\lambda$ to be the sum of its parts. That is, $\mathrm{size}(\lambda):=\sum\_{i=1}^{\infty}\lambda(i)=\sum\_{i=1}^{k}\lambda\_{i}$. We say that $\lambda$ is a partition of $n$, and write $\lambda\vdash n$, where $n=\mathrm{size}(\lambda)$.

We define the **length** of a partition $\lambda$ to be the number of nonzero parts in $\lambda$. That is, $\mathrm{length}(\lambda):=\max\\{i\in\mathbb{Z}\_{>0}|\lambda(i)\ne0\\}$. For $\lambda=(\lambda\_{1},\lambda\_{2},\ldots,\lambda\_{k})$ with $\lambda\_{1}\ge\lambda\_{2}\ge\ldots\ge\lambda\_{k}>0$, we have $\mathrm{length}(\lambda)=k$.

## Exercise

The [SageMath](https://sagemath.org) mathematics software system has some functionality for working with partitions built in. 

We can create a partition $p=(6,3,1)$ with the following command (case sensitive):

```python
p = Partition([6,3,1])
```

We can calculate $\mathrm{size}(p)=6+3+1=10$ and $\mathrm{length}(p)=3$ using the `size()` and `length()` methods respectively. These actually just make use of the built in functions `sum` and `len` for Python lists.

```python
p.size() # Equal to sum(p)
p.length() # Equal to len(p)
```

You can practice executing SageMath and Python code in the SageMathCell below.

<div class="sage">
  <script type="text/x-sage">
p = Partition([6,3,1]) # You can edit this code yourself
print("My partition p = {} has size(p) = {} and length(p) = {}".format(
p, p.size(), p.length()))
print(p.size() == sum(p))
print(p.length() == len(p))
  </script>
</div>

