+++
title = "Notation"
date =  2019-04-15T17:03:32+01:00
weight = 20
+++

## Alternative notation

Besides thinking of partitions as a sequence of summands (parts), we may encode the data in a handful of other ways. This can be useful for computation, compactness, or for realizing the appearance of partitions in other areas of mathematics and beyond.

In fact, the cycle of discovery often begins with mathematicians studying an object of interest in their own field, only later realizing that after a little bit of manipulation the problem at hand can also be viewed in terms of partitions.

### Exponential notation

The most simple alternative to describing a partition $\lambda$ by listing its parts $\lambda\_{j}$ is **exponential notation**, where instead we count the number of parts of size $i$ appearing in $\lambda$ for each positive integer $i$, that is $\alpha\_{i}=|\\{j\in\mathbb{Z}\_{>0}|\lambda(j)=i\\}|$, to form a finite sequence of nonnegative integers $\exp(\lambda):\mathbb{Z}\_{>0}\to\mathbb{Z}\_{\ge0}$ given by $\exp(\lambda)(i):=\alpha\_{i}$.

We usually write this as $\lambda=1^{\alpha\_{1}}2^{\alpha\_{2}}3^{\alpha\_{3}}\ldots\lambda\_{1}^{\alpha\_{\lambda\_{1}}}$ where $\lambda\_{1}=\max\\{i\in\mathbb{Z}\_{>0}|\alpha\_{\lambda}(i)\ne0\\}$ is called the **largest part** in $\lambda$, but may also directly write $\exp(\lambda)=(\alpha\_{1},\alpha\_{2},\alpha\_{3},\ldots,\alpha\_{\lambda\_{1}})$. For example:

<script type="text/tikz">
  \begin{tikzpicture}
    \begin{scope}[local bounding box=scope1]
      \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (4,-2);\draw (0,-3) -- (4,-3);\draw (0,-4) -- (2,-4);\draw (0,-5) -- (1,-5);\draw (1,0) -- (1,-5);\draw (2,0) -- (2,-4);\draw (3,0) -- (3,-3);\draw (4,0) -- (4,-3);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-5);
	\end{scope}
    \begin{scope}[font=\Large, shift={(-0.5,-0.5)}]
	  \draw (0,0) node{6};\draw (0,-1) node{4};\draw (0,-2) node{4};\draw (0,-3) node{2};\draw (0,-4) node{1};
	  \draw (-2.5,0) node{$1=\alpha_{6}$};\draw (-2.5,-0.75) node{$0=\alpha_{5}$};\draw (-2.5,-1.5) node{$2=\alpha_{4}$};\draw (-2.5,-2.25) node{$0=\alpha_{3}$};\draw (-2.5,-3) node{$1=\alpha_{2}$};\draw (-2.5,-4) node{$1=\alpha_{1}$};
	  \draw (-0.4,0) -- (-1.6,0);\draw (-0.4,-1) -- (-1.6,-1.5);\draw (-0.4,-2) -- (-1.6,-1.5);\draw (-0.4,-3) -- (-1.6,-3);\draw (-0.4,-4) -- (-1.6,-4);
    \end{scope}
    \begin{scope}[font=\Large, shift={(scope1.north)}]
	  \draw (0,1.2) node{$\lambda = (6,4,4,2,1)=1^{1}2^{1}3^{0}4^{2}5^{0}6^{1}$};
	  \draw (0,0.5) node{$\exp(\lambda)=(1,1,0,2,0,1)$};
    \end{scope}
  \end{tikzpicture}
</script>

We can obtain the exponential notation for a given partition in SageMath using the `to_exp()` method, and we can construct a partition from its exponential form using the `exp` keyword argument in the constructor.

```python
Partition([6,4,4,2,1]).to_exp()
# [1, 1, 0, 2, 0, 1]
Partition(exp=[1,1,0,2,0,1])
# [6, 4, 4, 2, 1]
```

### Frobenius Coordinates

The **Frobenius rank** of a partition $\lambda$ is given by the number of cells on the main diagonal of $\lambda$, and formally defined to be $\max\\{i\in\mathbb{Z}\_{>0}:\lambda\_{i}\ge i\\}$. This is also equal to the length of the largest square fitting into the Young diagram of $\lambda$. For example, the Frobenius rank of the partition $\lambda = (6,4,4,2,1)$ is $3$.

<script type="text/tikz">
  \begin{tikzpicture}
    \begin{scope}[local bounding box=scope1]
	  \filldraw[blue!5] (0,0) rectangle (1,-1);\filldraw[blue!5] (1,-1) rectangle (2,-2);\filldraw[blue!5] (2,-2) rectangle (3,-3);
      \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (4,-2);\draw (0,-3) -- (4,-3);\draw (0,-4) -- (2,-4);\draw (0,-5) -- (1,-5);\draw (1,0) -- (1,-5);\draw (2,0) -- (2,-4);\draw (3,0) -- (3,-3);\draw (4,0) -- (4,-3);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-5);
	\end{scope}
    \begin{scope}[font=\Large, shift={(0.5,-0.5)}]
	  \draw (0,0) node{1};\draw (1,-1) node{2};\draw (2,-2) node{3};
    \end{scope}
  \end{tikzpicture}
</script>

We can obtain the Frobenius rank for a given partition in SageMath using the `frobenius_rank()` method.

The **Frobenius coordinates** of a partition $\lambda$ of Frobenius rank $r$ is a pair of length-$r$ integer-valued vectors $p,q$ given by listing the [arm and leg](../visualization/#arms-legs-and-hooks) statistics, respectively, of the cells along the main diagonal in $\lambda$. That is, for $i=1,2,\ldots,r$

$$p\_{i}=a\_{\lambda}(i,i),q\_{i}=l\_{\lambda}(i,i).$$ 

For example, the diagram below illustrates how to obtain the Frobenius coordinates $p=(5,2,1)$, $q=(4,2,0)$ from the partition $\lambda = (6,4,4,2,1)$:

<script type="text/tikz">
  \begin{tikzpicture}
    \begin{scope}
	  \filldraw[blue!5] (0,0) rectangle (1,-1);\filldraw[blue!5] (1,-1) rectangle (2,-2);\filldraw[blue!5] (2,-2) rectangle (3,-3);
      \filldraw[red!15] (1,0) rectangle (6,-1);\filldraw[red!15] (2,-1) rectangle (4,-2);\filldraw[red!15] (3,-2) rectangle (4,-3);
	  \filldraw[green!15] (0,-1) rectangle (1,-5);\filldraw[green!15] (1,-2) rectangle (2,-4);
	\end{scope}
	\begin{scope}[black!20]
	  \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (4,-2);\draw (0,-3) -- (4,-3);\draw (0,-4) -- (2,-4);\draw (0,-5) -- (1,-5);\draw (1,0) -- (1,-5);\draw (2,0) -- (2,-4);\draw (3,0) -- (3,-3);\draw (4,0) -- (4,-3);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-5);
    \end{scope}
	\begin{scope}[font=\Large, local bounding box=scope1]  
	  \draw (0,0) -- (6,0);\draw (0,0) -- (0,-5);\draw (6,0) -- (6,-1);\draw (0,-1) -- (6,-1);\draw (0,-5) -- (1,-5);\draw (1,0) -- (1,-5);\draw (3.5, -0.5) node{5};\draw (0.5, -3.0) node{4};\draw (4,-1) -- (4,-2);\draw (1,-2) -- (4,-2);\draw (1,-4) -- (2,-4);\draw (2,-1) -- (2,-4);\draw (3.0, -1.5) node{2};\draw (1.5, -3.0) node{2};\draw (4,-2) -- (4,-3);\draw (2,-3) -- (4,-3);\draw (2,-3) -- (3,-3);\draw (3,-2) -- (3,-3);\draw (3.5, -2.5) node{1};\draw (2.5, -3.5) node{0};
    \end{scope}
  \end{tikzpicture}
</script>

We can obtain the Frobenius coordinates for a given partition in SageMath using the `frobenius_coordinates()` method, and we can also construct a partition using the `frobenius_coordinates` keyword argument in the constructor.

```python
Partition([6,4,4,2,1]).frobenius_coordinates()
# ([5, 2, 1], [4, 2, 0])
Partition(frobenius_coordinates=([5, 2, 1], [4, 2, 0]))
# [6,4,4,2,1]
```

Notice that if a partition $\lambda$ has Frobenius rank $r$, then for $i=1,2,\ldots,r-1$, its Frobenius coordinates $p,q$ must satisfy $p\_{i+1}\le p\_{i}-1$, and $q\_{i+1}\le q\_{i}-1$. That is to say, the Frobenius coordinates consist of strictly decreasing integer sequences of finite length.

{{%expand "Proof" %}} 
Let $\lambda$ be a partition, so $\lambda\_{i} - \lambda\_{i+1} \ge 0$. Therefore 

$$ p\_{i+1} - p\_{i} = a\_{\lambda}(i,i) - a\_{\lambda}(i+1,i+1) = \lambda\_{i}-i - (\lambda\_{i+1}-(i+1)) = \lambda\_{i} - \lambda\_{i+1} + 1 \ge 1.$$

Thus $p\_{i+1} - p\_{i} \ge 1$ and $p\_{i+1}\le p\_{i}-1$ as required. The proof is analogous for $q$ noting that the conjugate $\lambda'$ is also a partition.
{{% /expand%}}

If the Frobenius coordinates of a partition $\lambda$ is given by the pair $(p,q)\in\mathbb{Z}\_{\ge0}^{r}\times\mathbb{Z}\_{\ge0}^{r}$, then the Frobenius coordinates of its conjugate $\lambda'$ are given by the pair $(q,p)$. This follows from the deduction that $a\_{\lambda'}(i,j)=l\_{\lambda}(j,i)$, which we apply to the special case $i=j$, along with  the bijection $\mathrm{Young}(\lambda)\to\mathrm{Young}(\lambda')$ given by $(i,j)\mapsto(j,i)$ mentioned [earlier](../visualization/#cells).

### Maya diagrams, zero-one sequences, and Dyck words

In this section we introduce Maya diagrams, and explain their connection to partitions, Dyck paths from combinatorics, and the physical model known as "Dirac's electron sea".

Maya diagrams are used to visualize binary sequences of zeros and ones, and the two states 0 and 1 can be used to represent a wide range of paired notions, such as two directions when traversing a binary tree, two vectors in a basis of a 2D lattice, or a pair of oppositely charged particles (e.g. electrons and positrons).

#### Minimal zero-one sequences

We begin by explaining the `zero_one_sequence()` [method](https://doc.sagemath.org/html/en/reference/combinat/sage/combinat/partition.html#sage.combinat.partition.Partition.zero_one_sequence) for partitions in SageMath. We draw the Young diagram of a partition in [English notation](../visualization/conventions/) and label edges on its outer rim/boundary path according to the rule North=0 and East=1, and then read this 0-1 sequence from $(0, -\infty)$ to $(\infty, 0)$ so that part size increases as we read along the boundary path. 

Though such a sequence starts with infinitely many 0s and end with infinitely many 1s, the `zero_one_sequence()` method omits these to return a finite output, describing only the edges on the boundary of the Young diagram which do not lie on the axes. This may be called the _minimal_ 0-1 sequence of a partition.

Below we illustrate how to obtain the minimal zero-one sequence $(1,0,1,1,0,1,1,1,0)$ from the partition $\lambda=(6,3,1)$:

<script type="text/tikz">
  \begin{tikzpicture}
    \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (3,-2);\draw (0,-3) -- (1,-3);\draw (1,0) -- (1,-3);\draw (2,0) -- (2,-2);\draw (3,0) -- (3,-2);\draw (4,0) -- (4,-1);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-3);
    \draw[blue, ->] (0,-3) -- (1,-3);\draw[orange, ->] (1,-3) -- (1,-2);\draw[blue, ->] (1,-2) -- (2,-2);\draw[blue, ->] (2,-2) -- (3,-2);\draw[orange, ->] (3,-2) -- (3,-1);\draw[blue, ->] (3,-1) -- (4,-1);\draw[blue, ->] (4,-1) -- (5,-1);\draw[blue, ->] (5,-1) -- (6,-1);\draw[orange, ->] (6,-1) -- (6,-0);
	\begin{scope}[font=\Large]
	  \draw (0,-3) [below right] node{1};\draw (1,-3) [right] node{0};\draw (1,-2) [below right] node{1};\draw (2,-2) [below right] node{1};\draw (3,-2) [right] node{0};\draw (3,-1) [below right] node{1};\draw (4,-1) [below right] node{1};\draw (5,-1) [below right] node{1};\draw (6,-1) [right] node{0};
	\end{scope}
  \end{tikzpicture}
</script>

We can obtain the minimal zero-one sequence of a given partition in SageMath using the `zero_one_sequence()` method, and we can also construct a partition using the `zero_one` keyword argument in the constructor.

```python
Partition([6,3,1]).zero_one_sequence()
# [1, 0, 1, 1, 0, 1, 1, 1, 0]
Partition(zero_one=[1,0,1,1,0,1,1,1,0]) # Same as Partitions().from_zero_one([1,0,1,1,0,1,1,1,0])
# [6,3,1]
```

This leads to reading boundary paths from right to left in Russian and Cartesian notations.

#### Dyck paths

We will begin with an illustration of how to obtain the Maya diagram corresponding to a given partition before discussing the formal definitions and details. Just as with Young diagrams, Maya diagrams are also subject to choices of convention for how they relate to a particular partition, but for our purposes, we will fix the following convention:

#### States

Consider the set of integers $\mathbb{Z}$ as the disjoint union $\mathbb{Z}=\mathbb{\mathbb{Z}}\_{<0}\sqcup\mathbb{Z}\_{\ge0}$ of the negative integers $\mathbb{Z}\_{<0}$ and the nonnegative integers $\mathbb{Z}\_{\ge0}$. We define a **state** to be a subset $S\subset\mathbb{Z}$ such that the symmetric difference $S\Delta\mathbb{Z}\_{\ge0}$ is finite. That is, for $S^{C}:=\mathbb{Z}\setminus S=\\{n\in\mathbb{Z}|n\notin S\\}$

$$
S\Delta\mathbb{Z}\_{\ge0}=(S\setminus\mathbb{Z}\_{\ge0})\sqcup(\mathbb{Z}\_{\ge0}\setminus S)=(S\cap\mathbb{Z}\_{<0})\sqcup(S^{C}\cap\mathbb{Z}\_{\ge0})\,\text{finite.}
$$ 

We may identify a state $S\subset\mathbb{Z}$ with the pair of (necessarily) finite sets $(S\cap\mathbb{Z}\_{<0})$ and $(S^{C}\cap\mathbb{Z}\_{\ge0})$ by the bijection between 

$$
\\{S\subset\mathbb{Z}|S\Delta\mathbb{Z}\_{\ge0}\,\text{finite}\\} \leftrightarrow \\{(A,B)|A\subset\mathbb{Z}\_{\ge0}\,\text{finite},B\subset\mathbb{Z}\_{<0}\,\text{finite}\\}
$$

given by $S\mapsto(S^{C}\cap\mathbb{Z}\_{\ge0}$, $S\cap\mathbb{Z}\_{<0})$, with inverse given by $(A,B)\mapsto A^{C}\cap(B\cup\mathbb{Z}\_{\ge0})$.

{{%expand "Proof" %}}
For $S\subset\mathbb{Z}$ such that $S\Delta\mathbb{Z}\_{\ge0}$ is finite, let $(A,B):=(S^{C}\cap\mathbb{Z}\_{\ge0},S\cap\mathbb{Z}\_{<0})$, then $A\subset\mathbb{Z}\_{\ge0}$, $B\subset\mathbb{Z}\_{<0}$, and $S\Delta\mathbb{Z}\_{\ge0}=A\sqcup B$, so $A$, $B$ must both be finite. Moreover, 

$$ A^{C}\cap(B\cup\mathbb{Z}\_{\ge0}) = (S^{C}\cap\mathbb{Z}\_{\ge0})^{C}\cap((S\cap\mathbb{Z}\_{<0})\cup\mathbb{Z}\_{\ge0}) $$
$$ = (S\cup\mathbb{Z}\_{<0})\cap((S\cup\mathbb{Z}\_{\ge0})\cap(\mathbb{\mathbb{Z}}\_{<0}\cup\mathbb{Z}\_{\ge0})) $$
$$ = (S\cup\emptyset)\cap\mathbb{Z}=S $$

by De Morgan's laws and associativity and distributativity properties of union and intersection.

On the other hand, for finite subsets $A\subset\mathbb{Z}\_{\ge0}$, $B\subset\mathbb{Z}\_{<0}$, let $S=A^{C}\cap(B\cup\mathbb{Z}\_{\ge0})$, then $S^{C}=A\cup(B^{C}\cap\mathbb{Z}\_{<0})$, and so 

$$ S^{C}\cap\mathbb{Z}\_{\ge0} = (A\cup(B^{C}\cap\mathbb{Z}\_{<0}))\cap\mathbb{Z}\_{\ge0} $$
$$ = (A\cap\mathbb{Z}\_{\ge0})\cup((B^{C}\cap\mathbb{Z}\_{<0})\cap\mathbb{Z}\_{\ge0}) $$
$$ = A\cup\emptyset=A $$

as $A\subset\mathbb{Z}\_{\ge0}$, and also 

$$ S\cap\mathbb{Z}\_{<0} = (A^{C}\cap(B\cup\mathbb{Z}\_{\ge0}))\cap\mathbb{Z}\_{<0} $$
$$ = (A\cap\mathbb{Z}\_{<0}\cap B)\cup(A\cap\mathbb{Z}\_{<0}\cap\mathbb{Z}\_{\ge0}) $$
$$ = A\cap\mathbb{Z}\_{<0}\cap B=B $$

as $B\subset\mathbb{Z}\_{<0}=(\mathbb{Z}\_{\ge0})^{C}\subset A^{C}$, as $A\subset\mathbb{Z}\_{\ge0}$. Therefore $S\Delta\mathbb{Z}\_{\ge0}=(S^{C}\cap\mathbb{Z}\_{\ge0})\sqcup(S\cap\mathbb{Z}\_{<0})=A\sqcup B$ is finite.
{{% /expand%}}

#### Zero-one sequences

A **Maya diagram** is a function $\mathrm{\boldsymbol{m}}:\mathbb{Z}\to\\{0,1\\}$ such that there exist $N,M\in\mathbb{Z}$ such that for all $\nu>N$ we have $\boldsymbol{\mathrm{m}}(\nu)=1$ and for all $\nu<M$ we have $\boldsymbol{\mathrm{m}}(\nu)=0$. It follows that $M\le N+1$.

Let $S\subset\mathbb{Z}$ be a state, then its identity function $\mathbb{1}\_{S}:\mathbb{Z}\to\\{0,1\\}$, 

$$\mathbb{1}\_{S}(\nu) = \begin{cases} 1 & \nu\in S\\\\ 0 & \nu\notin S \end{cases}$$

is a Maya diagram, where we may take $N=\max(S^{C}\cap\mathbb{Z}\_{\ge0})$, $M=\min(S\cap\mathbb{Z}\_{<0})\in\mathbb{Z}$. 
 
On the other hand, for a Maya diagram $\mathrm{\boldsymbol{m}}:\mathbb{Z}\to\\{0,1\\}$ we may define a state $S=\boldsymbol{\mathrm{m}}^{-1}(1)=\\{\nu\in\mathbb{Z}|\boldsymbol{\mathrm{m}}(\nu)=1\\}$, in which case 
 
$$ |S\cap\mathbb{Z}\_{<0}|=|\\{\nu\in\mathbb{Z}\_{<0}|\mathrm{\boldsymbol{m}}(\nu)=1\\}|\le\max(0,-M) $$ 

and 

$$ |S^{C}\cap\mathbb{Z}\_{\ge0}|=|\\{\nu\in\mathbb{Z}\_{\ge0}|\boldsymbol{\mathrm{m}}(\nu)=0\\}|\le\max(0,N+1).$$ 

{{%expand "Proof" %}}
Let $\mathrm{\boldsymbol{m}}:\mathbb{Z}\to\\{0,1\\}$ be a Maya diagram such that $\boldsymbol{\mathrm{m}}(\nu)=1$ for all $\nu>N$, and $\boldsymbol{\mathrm{m}}(\nu)=0$ for all $\nu<M$. Let $S=\boldsymbol{\mathrm{m}}^{-1}(1)=\\{\nu\in\mathbb{Z}|\boldsymbol{\mathrm{m}}(\nu)=1\\}$. Then 

$$ S\cap\mathbb{Z}\_{<0} = \\{\nu\in\mathbb{Z}\_{<0}|\mathrm{\boldsymbol{m}}(\nu)=1\\} \subset \\{\nu\in\mathbb{Z}|M\le\nu<0\\} $$

and 

$$ S^{C}\cap\mathbb{Z}\_{\ge0} = \\{\nu\in\mathbb{Z}\_{\ge0}|\boldsymbol{\mathrm{m}}(\nu)=0\\} \subset \\{\nu\in\mathbb{Z}|0\le\nu\le N\\}. $$
{{% /expand%}}

We define the **charge** of a Maya diagram/state to be the difference 
 
$$ \mathrm{charge}(S)=|S^{C}\cap\mathbb{Z}\_{\ge0}|-|S\cap\mathbb{Z}\_{<0}|=|\boldsymbol{\mathrm{m}}^{-1}(0)\cap\mathbb{Z}\_{\ge0}|-|\boldsymbol{\mathrm{m}}^{-1}(1)\cap\mathbb{Z}\_{<0}|.$$

### Beta numbers

Beta numbers have applications in Representation theory.

## Interchanging between notations

We can prove that these notations are equivalent and that we can freely interchange between them, i.e. that the set of partitions is in bijection with the set of e.g. Frobenius coordinates

We also demonstrate and explain how these have been implemented in SageMath

```python
# Insert code here
```




