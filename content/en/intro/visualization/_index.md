+++
title = "Visualization"
date =  2019-04-15T17:03:32+01:00
weight = 10
+++

## Graphical representations

Now that we've given a few basic definitions, it's time to appreciate the fact that we can think about partitions visually and thus utilize our natural spatial intuition to further understand them, rather than only thinking of them as sequences of numbers.

The two most commonly used methods of representing partitions with diagrams are Ferrers diagrams and Young diagrams. We will discuss other diagrammatic representations later.

### Ferrers diagrams (English notation)

To represent a partition as a **Ferrers diagram** we draw a row of dots for each part in the partition and stack them from top to bottom in descending order, i.e. longest row/largest part at the top, aligned to the upper-left corner (of the 4th quadrant). For example, the Ferrers diagram for the partition $\lambda = (6,3,1)$ is given by

<script type="text/tikz">
  \begin{tikzpicture}
    \filldraw (0,0) circle (.2);\filldraw (1,0) circle (.2);\filldraw (2,0) circle (.2);\filldraw (3,0) circle (.2);\filldraw (4,0) circle (.2);\filldraw (5,0) circle (.2);\filldraw (0,-1) circle (.2);\filldraw (1,-1) circle (.2);\filldraw (2,-1) circle (.2);\filldraw (0,-2) circle (.2);
  \end{tikzpicture}
</script>

We can use the `ferrers_diagram()` method to return the Ferrers diagram of a partition as a string, and we can use the `pp()` method to print the Ferrers diagram to the display.

```python
mu = Partition([6,3,1])
print(type(mu.ferrers_diagram()))
mu.pp() # Runs print(mu.ferrers_diagram()), returns None
```

### Young diagrams and Young tableaux

A **Young diagram** is very similar to a Ferrers diagram except we draw rows of boxes instead of dots. For example, we display the Young diagram for the partition $\lambda = (6,3,1)$ below.

<script type="text/tikz">
  \begin{tikzpicture}
    \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (3,-2);\draw (0,-3) -- (1,-3);\draw (1,0) -- (1,-3);\draw (2,0) -- (2,-2);\draw (3,0) -- (3,-2);\draw (4,0) -- (4,-1);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-3);
  \end{tikzpicture}
</script>

Young diagrams are a more useful way of visualizing partitions because we can fill the boxes (cells) with numbers (or other data) to obtain Young tableux.

## Cells

We call each box (resp. dot) in a Young (resp. Ferrers) diagram a **cell** in the diagram, with coordinates $(i,j)$ for the cell in the $i$-th row and $j$-th column of a partition. For a partition $\lambda=(\lambda\_{1},\lambda\_{2},\ldots,\lambda\_{k})$ we identify its Young diagram with the set of cells $$\mathrm{Young}(\lambda) = \\{(i,j)|1 \le i \le k, 1 \le j \le \lambda\_{i}\\}$$

Let $\lambda = (6,3,1)$. We highlight the cells $s = (1,3), t = (2,3) \in \mathrm{Young}(\lambda)$ in the diagram below

<script type="text/tikz">
  \begin{tikzpicture}
    \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (3,-2);\draw (0,-3) -- (1,-3);\draw (1,0) -- (1,-3);\draw (2,0) -- (2,-2);\draw (3,0) -- (3,-2);\draw (4,0) -- (4,-1);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-3);
    \begin{scope}[font=\Large]
	  \draw (2.5, -0.5) node{s};\draw (2.5, -1.5) node{t};
	\end{scope}
  \end{tikzpicture}
</script>

We can obtain the coordinates of the cells in a partition as a list using the `cells()` method, but note that in Python/SageMath that indices are $0$-based (i.e. indices start from $0$ instead of $1$).

```python
Partition([6,3,1]).cells()
# [(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (1, 0), (1, 1), (1, 2), (2, 0)]
```

It should be clear that the size of a partition $\lambda$ is equal to the number of cells in its Young diagram, that is $\mathrm{size}(\lambda) = |\mathrm{Young}(\lambda)|$, and that we can recover the parts of a partition from its Young diagram by counting the number of cells in the corresponding row: $\lambda\_{i} = |\\{(i,j)\in\mathrm{Young}(\lambda)\\}| = \max\\{j:(i,j)\in\mathrm{Young}(\lambda)\\}$.

Notice that the way we index cells in the diagrams above is the same way as we index entries in matrices, first by rows and then by columns. This way of doing things is called **English notation** and is the most commonly used in the literature.

## Variations in conventions

We will introduce three other ways to draw Young diagrams: French notation, Russian notation, and Cartesian notation. Let $\lambda = (6,3,1)$. We highlight the cells $s = (1,3), t = (2,3) \in \mathrm{Young}(\lambda)$ below using each of these conventions in turn.

### French notation

**French notation** relates to English notation by a reflection in the $x$-axis, i.e. stack parts in rows with index increasing from bottom to top, i.e. longest row/largest part at the bottom, aligned to the bottom-left corner of the 1st quadrant.

<script type="text/tikz">
  \begin{tikzpicture}
    \draw (0,0) -- (6,0);\draw (0,1) -- (6,1);\draw (0,2) -- (3,2);\draw (0,3) -- (1,3);\draw (1,0) -- (1,3);\draw (2,0) -- (2,2);\draw (3,0) -- (3,2);\draw (4,0) -- (4,1);\draw (5,0) -- (5,1);\draw (6,0) -- (6,1);\draw (0,0) -- (0,3);
    \begin{scope}[font=\Large]
	  \draw (2.5, 0.5) node{s};\draw (2.5, 1.5) node{t};
	\end{scope}
  \end{tikzpicture}
</script>

### Russian notation

**Russian notation** may be obtained by rotating a diagram drawn using English notation anticlockwise 135 degrees, and can motivate Maya diagrams which will be descussed later.

<script type="text/tikz">
  \begin{tikzpicture}
    \begin{scope}[scale=0.7071, font=\Large]
	\draw (0,0) -- (-6,6);\draw (1,1) -- (-5,7);\draw (1, 0) node{6};\draw (2,2) -- (-1,5);\draw (2, 1) node{3};\draw (3,3) -- (2,4);\draw (3, 2) node{1};\draw (0,0) -- (3,3);\draw (-1,1) -- (2,4);\draw (-2,2) -- (0,4);\draw (-3,3) -- (-1,5);\draw (-4,4) -- (-3,5);\draw (-5,5) -- (-4,6);\draw (-6,6) -- (-5,7);
	\draw (-2, 3) node{s};\draw (-1, 4) node{t};
	\end{scope}
  \end{tikzpicture}
</script>

### Cartesian notation

Sometimes we will use a convention obtained by rotating a diagram drawn using English notation anticlockwise 90 degrees, which we will call 'Cartesian' notation. In **Cartesian notation** the diagrams are aligned to the bottom-left corner of the 1st quadrant, and parts correspond to columns which decrease in size from left to right. The $(i,j)$ coordinates for cells resemble the standard Cartesian coordinates $(x,y)$ for the Euclidean plane.

<script type="text/tikz">
  \begin{tikzpicture}
    \draw (0,0) -- (0,6);\draw (1,0) -- (1,6);\draw (2,0) -- (2,3);\draw (3,0) -- (3,1);\draw (0,1) -- (3,1);\draw (0,2) -- (2,2);\draw (0,3) -- (2,3);\draw (0,4) -- (1,4);\draw (0,5) -- (1,5);\draw (0,6) -- (1,6);\draw (0,0) -- (3,0);
    \begin{scope}[font=\Large]
	  \draw (0.5, 2.5) node{s};\draw (1.5, 2.5) node{t};
	\end{scope}
  \end{tikzpicture}
</script>

## Conjugation

The **conjugate** of the partition $\lambda$ is the partition $\lambda'$ obtained by swapping the rows and columns in the Young diagram. Formally, $\lambda'(j):=|\\{i:\lambda(i)\ge j\\}|$ for each $j\in \mathbb{Z}\_{>0}$. This is also called the associated partition or the transpose in the literature.

For example, if $\lambda = (6,3,1)$, then its conjugate is given by $\lambda'=(3, 2, 2, 1, 1, 1)$.

<script type="text/tikz">
  \begin{tikzpicture}
    \begin{scope}[shift={(-7,0)}, local bounding box=scope1]
      \draw (0,0) -- (6,0);\draw (0,-1) -- (6,-1);\draw (0,-2) -- (3,-2);\draw (0,-3) -- (1,-3);\draw (1,0) -- (1,-3);\draw (2,0) -- (2,-2);\draw (3,0) -- (3,-2);\draw (4,0) -- (4,-1);\draw (5,0) -- (5,-1);\draw (6,0) -- (6,-1);\draw (0,0) -- (0,-3);
    \end{scope}
    \begin{scope}[font=\Large, shift={(scope1.north)}]
	  \draw (0,0.5) node{$\lambda = (6,3,1)$};
    \end{scope}
    \begin{scope}[shift={(5,0)}, local bounding box=scope2]
      \draw (0,0) -- (3,0);\draw (0,-1) -- (3,-1);\draw (0,-2) -- (2,-2);\draw (0,-3) -- (2,-3);\draw (0,-4) -- (1,-4);\draw (0,-5) -- (1,-5);\draw (0,-6) -- (1,-6);\draw (1,0) -- (1,-6);\draw (2,0) -- (2,-3);\draw (3,0) -- (3,-1);\draw (0,0) -- (0,-6);
    \end{scope}
    \begin{scope}[font=\Large, shift={(scope2.north)}]
      \draw (0,0.5) node{$\lambda'=(3, 2, 2, 1, 1, 1)$};
    \end{scope}
    \begin{scope}[font=\Large, shift={(0,-2)}]
      \draw (2, 1) node{conjugation};
      \draw[->] (0,0.5) -- (4,0.5);
      \draw[->] (4,0) -- (0,0);
	\end{scope}
  \end{tikzpicture}
</script>

We can calculate the conjugate of a partition in SageMath using the `conjugate()` method or the helper function of the same name.

```python
Partition([5,5,3,2,1]).conjugate() # Same as conjugate(Partition([5,5,3,2,1])) 
# [5, 4, 3, 2, 2]
```

You can practice executing SageMath and Python code in the SageMathCell below.

<div class="sage">
  <script type="text/x-sage">
mu = Partition([6,3,1]) # You can edit this code yourself
print(type(mu.ferrers_diagram()))
mu.pp()
print(Partition([5,5,3,2,1]).conjugate())
print(conjugate(Partition([5,5,3,2,1])))
print(type(Partition([5,5,3,2,1]).conjugate()))
print(type(conjugate(Partition([5,5,3,2,1]))))
  </script>
</div>