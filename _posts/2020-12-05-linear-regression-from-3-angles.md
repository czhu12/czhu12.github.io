---
layout: post
title: Linear Regression from 3 Angles
---
Linear regression is a technique that can be viewed from a few different perspectives.

Its usually framed as:

```
Y = y_ + aX
```

Let's work with this dataset to illustrate our discussion:

```
x1 | y
1  | 1
2  | 2
3  | 2
```

Clearly, there is no solution in the form of Y = a + bX for this data.

[TODO: Draw graph here]

### Linear Algebra
The problem above can be reframed as:

Ax = b

Where A = 1 2
          1 2
          1 3

      b = 1
          2
          2

      x = [a b]

Where the goal is to find the values for x that *best* solves the solution.

The *best* solution in the column space of A. **To put this another way, we want to find the projection of b onto the A plane.**

So, the new question is: How do we find the projection of a vector onto a plane?

In the diagram above, we can break the vector into the addition of two components: The projection component and the error component.

This lands us onto the famous equation:


### Statistics
Linear regression can instead be framed from a probabilistic perspective.
