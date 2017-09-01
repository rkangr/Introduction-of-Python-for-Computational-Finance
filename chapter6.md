---
title       : Matrices
description : Introduction to working with matrix elements

--- type:NormalExercise lang:python xp:100 skills:2 key:ad0c054fea
## Matrices
We have already learned how to use vectors but sometimes it can be more convenient to arrange the data into matrices i.e. have several vectors next to each other.

1) There are many ways to create a matrix in Python (when the package numpy is used). For this course it is enough to know how to do that with the commands np.zeros(), np.ones() and np.array(). We have seen, how to create vectors with those commands. To create matrices (or multidimensional arrays) we just have to indicate, how many values each index of the matrix can take. For matrices of zeros or ones this can be done with providing the parameter shape as follows: `np.zeros(shape=[5,3])` generates a matrix with 5 rows and three columns, `np.ones(shape=[2,3,5])` generates a three-dimensional array of ones of the size 2x3x5 elements. We can generate a matrix with given values with the command `array()` by providing elements by rows in the form `np.array([[1.5,0,3],[0,0.5,5]])` (a 2x3 matrix)

Remark: Of course a matrix can also be the output of some function so this is yet another example of producing a matrix.

2) What might we do with a matrix? We could add or subtract or multiply or divide or compare them element-wise as we did with vectors using the same operators as long as the matrices have matching dimensions. There is a function for matrix multiplication (the function `np.dot()`), but we do not need to use it in the course.

3) The principle of extracting elements from a matrix is a generalization of the concept of extracting elements from a vector and again makes use of the square brackets. The difference is that now there are two positions inside the brackets -- first for rows and the other for columns. We still have to keep in mind that the numbering of rows and columns starts from 0. Let us first define

`M=np.array([np.linspace(0,1,10),np.arange(-3,7),2**np.arange(1,11)])`

and then we can

- ask for  the element in the 2nd row and 3rd column with M[1,2]
- ask for all the elements in the first row with M[0,:]
- ask for all the elements in the 4th column with M[:,3]
- ask for all the elements in the 1st column except the one in the first row with M[1:, 0]
- ask for the 1st and 3rd elements in the 1st row with M[0, np.array([0,2])]
- ask for the submatrix that consists of rows with indexes 1 and 2 (second and third) and columns with indexes 2 and 3 with M[1:3,2:4]
- ask for all the elements in the matrix that are greater than 1 with M[M>1]
- ask for elements of a matrix at specified positions by providing vectors containing corresponding first and second indexes:

```python
i=np.array([0,1,2])
j=i+1
M[i,j]
```
produces a vector with elements $M$<sub>01</sub>,$M$<sub>12</sub>,$M$<sub>23</sub>

We can use all previous constructs for assigning values for some elements of a matrix, but we have to be careful to provide a suitable right hand side (a scalar is always OK, but a vector or matrix has to be with correct dimensions) So 

```python
M[:,1]=10
M[2,1:5]=np.array([3,4,5,6])
```

are correct, but 

```python
M[1:,0]=np.arange(0,3)
```
does not work, since we try to assign to two matrix elements a vector with three values
Remark: As we see from example 7, it is possible to use a logical matrix to specify the positions from which we want to extract the elements. However, as this does not follow the usual square brackets extraction style for matrices (there is no comma inside), both the logical matrix and the matrix that we are extracting the data from are first converted into a vector and the output will also be a vector (even if it could theoretically have a matrix layout).


*** =instructions
- Make a 3x3 matrix X filled with elements 2,3,4,...,10 row by row. 
- Set all element of the second column of X to be equal to 0
- Fill the main diagonal of X with numbers 3,2,1 (so that X<sub>00</sub>=3,X<sub>11</sub>=2,X<sub>22</sub>=1)
- Write a command that sets the elements of X that are above the main diagonal (ie elements of the form X<sub>i,i+1</sub> to be equal to 5
- Replace the values of the second row of X with the sum of the corresponding values of the first and the third row and then print the final result.

*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
#import numpy

#define X with given values

#set the second column to be 0

#set the main diagonal to the correct values 

#set the values above the main diagonal to be equal to 5

#replace the second row with the sum of first and third rows

#print out the final matrix X

```

*** =solution
```{python}
#import numpy
import numpy as np
#define X with given values
X=np.array([[2,3,4],[5,6,7],[8,9,10]])
#set the second column to be 0
X[:,1]=0
#set the main diagonal to the correct values 
i=np.arange(0,3);X[i,i]=np.array([3,2,1])
#set the values above the main diagonal to be equal to 5
i=np.array([0,1]);X[i,i+1]=5
#replace the second row with the sum of first and third rows
X[1,:]=X[0,:]+X[2,:]
#print out the final matrix X
print(X)

```

*** =sct
```{python}
Ex().check_object('X').has_equal_value()

```
