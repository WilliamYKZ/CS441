# Numpy Question

```python
%matplotlib inline
import matplotlib.pyplot as plt
import numpy as np
```



## Task: Floating point operation

1. it will hang your notebook since we should not try check for ecact equivalence (==) with floats. we can meansure approximate equivalence. 

   ```python
   fp = 0
   while fp != 1:
       fp = fp +0.1
   ```



2. Also, be careful about adding very small increments to a large-magnitude number. if you continuously add a small amount to a large float, you will notice that the float eventually stops changing at all.

   ```python
   x = 10.0**200 # 10 to the power of 200
   y = x + 1
   if x == y:
       print("x is still the same as y")
   
   # x is still the same as y
   ```



3. In python some time the floating point number x,y,z. (x  + y) + z != x + (y  + z)

   ```python
   x = 498
   y = 1e100
   z = -1e100
   
   #the small magnitude of 498 relative to 1e100 makes the 498 disappear in x+y:
   
   assert (x + y) + z != x + (y + z), "Incorrect counter-example: LHS equals RHS"
   print("Good counter-example!")
   ```



4. Also in python sometime the floating point number a,b,c a * (b + c) != a * b + a * c

   ```python
   a = 100
   b = 0.1
   c = 0.2
   assert a * (b + c) != a * b + a * c, "Incorrect counter-example: LHS equals RHS"
   print("Good counter-example!")
   ```



5. There are not equivalent in Python's floating point representation.

   ```python
   if .3 != .1 * 3:
       print("Floating point numbers are weird.")
   ```





## Task: Basic Operations

1. Some basic operations

   ```python
   a_mul_b = a * b
   a_plus_b = a + b
   a_minus_b = a - b
   a_div_b = a / b
   a_pow_b = a ** b
   ```



## Task: Element-wise Array Functions

Question: Can we write this fucntion using python.
$$
f\left(a_{i}\right)=\log \left(\frac{a_{i}}{10-a_{i}}\right)+\sin \left(a_{i}\right)
$$

1. Numpy offers comprehensive mathematical functions.

   ```python
   a = np.array([1,2,3])
   f = np.log(a/(10-a)) + np.sin(a)
   print (f)
   ```



## Task: Left multiply a matrix with a diagonal matrix

Description: Assume a numpy array $A$ with shape $(n,m)$ is given as well as a numpy array $a$ with shape $(n,)$. we want to find a matrix $B$ such that. 
$$
B=\left[\begin{array}{cccc}
a_{1} & 0 & \cdots & 0 \\
0 & a_{2} & \ldots & 0 \\
\vdots & \vdots & \ddots & 0 \\
0 & 0 & \ldots & a_{n}
\end{array}\right] \times A
$$
where $a_1,....,a_n$ are the elements in $a$.

write a function `dial_left_mult` which takes the two arrays $a$ and $A$ as above and returns the matrix $B$. 

1. Solution 1

   ```python
   def diag_left_mult(a,A):
       
       a_diag = np.diag(a)
       
       return a_diag @ A
    
   a = np.array([1,2])
   A = np.array([[1,2],[3,4]])
   print (A)
   diag_left_mult(a,A)
   ```

   **Note that we have used the `@` operator for matrix multiplication.**



2. Solution 2

   ```python
   def diag_left_mult(a,A):
       return a.reshape(-1, 1) * A
     
   a = np.array([1,2])
   A = np.array([[1,2],[3,4]])
   diag_left_mult(a,A)
   ```

   The -1 argument with reshape will act as a wildcard for the appropriate number of missing dimensions. In this case, `a.reshape(-1, 1)` is the same as `a.reshape(2, 1)`.



## Task: Geometric Mean of an array

Description: Assume that you have a numpy array $a$ with shape $(d,)$, how can we find the geometric mean of the element in $a$? Remember that if the elements of $a$ are $(a_1,...,a_n)$, the geometric mean is $\sqrt[n]{a_1\times ...\times a_n}$.

Write a function it input a numpy array $a$ with shape $(d,)$. Do not assume anything about $d$ other than it is a positive integer. Also, do not assume anything about the element of $a$ other than they are positive values.

Output: a single value, which is the geometric mean of the elements in $a$.

```python
def geom_mean(a):
  d = a.shape[0]
  prod = np.prod(a)
  return prod**(1/d)

a = np.array([1,2,3])
geom_mean(a)
```



### `np.shape`

```python
import numpy as np

x = np.array([ [67, 63, 87],
             [77, 69, 59],
             [85, 87, 99],
             [68, 92, 78],
             [63, 89, 93]  ])
print(np.shape(x))

# it will return (6,3)
```





## Task: adjusting the elements in a matrix

Description: Given a numpy array $A$ with shape $(n,m)$, we want to generate another matrix $B$ with the same shape such that.
$$
B_{i, j}=A_{i, j} * i / j \quad 1 \leq i \leq n, 1 \leq j \leq m
$$
Example: if 
$$
A=\left[\begin{array}{lll}
3 & 2 & 1 \\
6 & 5 & 4
\end{array}\right]
$$
then
$$
B=\left[\begin{array}{lll}
3 \times 1 / 1 & 2 \times 1 / 2 & 1 \times 1 / 3 \\
6 \times 2 / 1 & 5 \times 2 / 2 & 4 \times 2 / 3
\end{array}\right]=\left[\begin{array}{ccc}
3 & 1 & 0.33 \\
12 & 5 & 2.66
\end{array}\right]
$$
Write a function `matrix_manipulate_1` which takes a numpy array $A$ as above, and outputs a numpy array $B$ as above.

```python
def matrix_manipulate_1(A):
  (n,m) = A.shape
  row_multipiers = (1 + np.arange(n)).reshape(-1,1)
  column_divisors = (1+np.arange(m)).reshape(1,-1).astype(np.float64)
  
  B1 = A * row_multipliers
  B = B1 / column_divisors
  return B

A = np.array([[3,2,1],[6,5,4]])
matrix_manipulate_1(A)
```





## Task: NumPy basic indexing

1. Basic indexing involves selecting specific elements in arrays and slicing arrays.
