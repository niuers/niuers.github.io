---
title: "Matrix Related Problems"
date: 2021-07-29
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - matrix
  - summary
---

1. Rotate a matrix by 90 degree
    1. You can rotate the matrix in a group of 4
    2. The most elegant solution for rotating the matrix is to firstly reverse the matrix around the main diagonal (matrix transpose), and then reverse it from left to right. These operations are called transpose and reflect in linear algebra.

2. Spiral Matrix
    1. Follow the path
        * How do you turn in direction?
            * Create a direction array, `[(0, 1), (1, 0), (0, -1), (-1, 0)]`, then you can use `direction = (direction+1)%4` to turn right, moving from right, to down, to left and to up, etc. 
            * You can initialize `direction_x, direction_y = 0,1`, and turn right use `direction_x, direction_y = direction_y, -direction_x`
    2. Do it layer-by-layer: We define the `k-th` outer layer of a matrix as all elements that have minimum distance to some border equal to `k`. Then you can use the top-left and bottom-right coordinates to specify the layer.
        * We can observe that, for any given `n`, the total number of layers is given by : `⌊(n+1)/2⌋`. This works for both even and odd `n`.


3. Search in a sorted matrix
    1. Iterate over the diagonal. let `m` denotes the number of rows and `n` denotes the number of columns.
        * Search the target element by element `O(m+n)`: start from top right or bottom left.
        * Search the target using binary search `O(log n!)=O(n log n)`: each time search the sub-matrix from current `i-th` diagonal.
    2. Divide and Conquer: We can partition a sorted two-dimensional matrix into four sorted submatrices, two of which might contain target and two of which definitely do not. `O(nlogn)`
        * we seek along the matrix's middle column  `mid` for an index `row` such that `matrix[row-1][mid] < target < matrix[row][mid]`




[LC48. Rotate Image]: https://leetcode.com/problems/rotate-image/
[LC54. Spiral Matrix]: https://leetcode.com/problems/spiral-matrix/
[LC59. Spiral Matrix II]: https://leetcode.com/problems/spiral-matrix-ii/
[LC240. Search a 2D Matrix II]: https://leetcode.com/problems/search-a-2d-matrix-ii/



    


