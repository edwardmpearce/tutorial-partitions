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

The **Frobenius coordinates** of a partition $\lambda$ of Frobenius rank $r$ is a pair of length-$r$ vectors $p,q$ given by listing the [arm and leg](../visualization/#arms-legs-and-hooks) statistics, respectively, of the cells along the main diagonal in $\lambda$. That is, for $i=1,2,\ldots,r$

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

We also discuss Frobenius coordinates, Maya diagrams (zero-one sequences), and Dyck words.

### Maya diagrams and zero-one sequences

## Interchanging between notations

We can prove that these notations are equivalent and that we can freely interchange between them, i.e. that the set of partitions is in bijection with the set of e.g. Frobenius coordinates

We also demonstrate and explain how these have been implemented in SageMath

```python
# Insert code here
```




