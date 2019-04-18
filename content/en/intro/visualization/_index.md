+++
title = "Visualization"
date =  2019-04-15T17:03:32+01:00
weight = 10
+++

## Graphical representations

Now that we've given a few basic definitions, it's time to appreciate the fact that we can think about partitions visually and thus utilize our natural spatial intuition to further understand them, rather than only thinking of them as sequences of numbers.

The two most commonly used methods of representing partitions with diagrams are Ferrers diagrams and Young diagrams. We will discuss other diagrammatic representations later.

<script type="text/tikz">
  \begin{tikzpicture}
    \draw (0,0) -- (0,6);\draw (1,0) -- (1,6);\draw (2,0) -- (2,3);\draw (3,0) -- (3,1);\draw (0,1) -- (3,1);\draw (0,2) -- (2,2);\draw (0,3) -- (2,3);\draw (0,4) -- (1,4);\draw (0,5) -- (1,5);\draw (0,6) -- (1,6);\draw (0,0) -- (3,0);
  \end{tikzpicture}
</script>

Young diagrams are a more useful way of visualizing partitions because we can fill the boxes (cells) with numbers to obtain Young tableux.

## Diagram conventions

Notice that in the above diagram we chose to have our partition placed into the corner of the positive quadrant. This is what we will call the 'Cartesian' convention, but it is not widely used in the literature.

The notations most commonly used in the literature are English notation where indexing is the same as for matrices (rows, columns); French notation; and Russian notation.

We can produce Ferrers diagrams using SageMath as follows, and may choose our preferred output notation using the options.

```python
# Insert code here
```




