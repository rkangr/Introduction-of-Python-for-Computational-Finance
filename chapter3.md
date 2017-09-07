---
title       : Manipulating vectors
description : Some basic operations with NumPy vectors

--- type:NormalExercise lang:python xp:100 skills:2 key:37e0df6c79
## Using vectors

When we have created vectors our aim is typically to make use of them. Many functions can be used.

1) + - * / **   % are examples of binary operators (performing addition, subtraction, multiplication, division, raising to a power, division, integer division remainder, respectively). They all operate elementwise as do most of the functions in the NumPy and SciPy packages of Python.  
For example after creating 

```python
x=np.array([3.4,7]) 
y=np.array([1,5])
```
we can write
`x+y`
to get a vector with elements 4.4,12 as a result and `x/y` to get a vector with elements 3.4,1.4. The vectors that we are going to use should have the same length (or at least one of them should be an single number). 

2)Examples of (element-wise) operators producing logical vectors are `==` `>=` `>` `<` `<=` `!=` (respectively equal to, greater than or equal to, greater than, less than, less than or equal to and not equal to.  For example
x>y 
returns True,True as both elements of x are greater than the respective elements of y. 
It is also interesting that logical vectors can be used in arithmetic operations like 5+3*(x>4). Python simply translates True to 1 and False to 0.

3) Some functions use all the elements in the input vector to produce a single number as a result. For example
`np.mean(x)`
produces 4.2, `np.any(x>4)` returns True (since at least one of the values of the logical vector `x>4` is True) and `np.all(x>4)` returns False (since at least one of the values of `x>4` is False)

4)We might need just some elements of a vector. This is accomplished with square brackets and using indexes, index arrays or slicing notatins. Slicing notations allows to specify in the square brackets the starting index, ending index (which is not included!) and an optional increment (the step between consecutive indexes used with default value of 1; can also be negative if we want to move in negative direction). So `x[start:end:step]` denotes elements of `x` with indexes `start`, `start+step`, `start + 2*step` and so on, which are smaller than `end` (index `end` is not used!). Negative `start` or `end` specify distance from the end of the array. If `start` of `end` are not specified, they are taken so that maximal number of indexes is returned - if `step` is positive, then missing start means that elements with indexes starting from 0 are selected and in the case of missing end all possible indexes of the form `start+step` are used; in the case of negative `step`, missing `start` means that selected indexes start from the last element of the array and missing `end` means, that again all idexes of the form `start+step` are used.

Let us define
`x=np.arange(2,11)`
`y=np.arange(9,0,-1)`
It is imprtant to remember that in Python the elements of a vector are numbered starting from 0. Thus we can

- ask for the third element in vector y with `y[2]`
- ask for the third, fourth and fifth element of y by `y[2:5]` (note that the first number is the index of the first element we want and the second number is the index of the first element we don't want, ie the element with index 5 is not included)
- ask for the first three elements in y with `y[:3]` (missing starting index is taken to be 0)
- ask for the last four elements in y with `y[-4:]` (negative number denotes counting from the end)
- ask for the first four elements in x in the reverse order by `x[3::-1]`
- ask for the second, fourth and sixth element from `x` with
`x[np.array([1,3,5])]`
- ask for specific elements from `x` by specifying the required elements by a logical vector which is created using a condition like  `x[y>4]` or `x[(x>3)&(x<5)]`
- write an index after any expression that produces a vector, for example (x-y)[2] and np.sqrt(x)[3] are valid usages of indexes.

5) Replacing elements in a vector is possible by first selecting the elements that need replacing (as shown previously) and then writing the replacements on the other side of the equality sign. For example
`y[1:6]=np.array([1,3,11,2,9])`
replaces the five elements starting from the second one in the vector y by 1,3,11,2,9 respectively.

6) Sometimes we need to save the current values of a vector for later use before modifying them. The correct way is to use a command of the form
`y=x.copy()`
If one uses `y=x`, then `y` and `x` are just two different names for the same memory location (`y` is an alias or nickname of `x`) and if you modify the value of one, the value of the other one also changes. Execute the commands 

```python
import numpy as np
x=np.arange(5)
y=x.copy()
z=x
x[2]=10
z[-1]=0
```
in the Ipython shell and check what happened to the values of `x`, `y` and `z`. Do you see the difference?
*** =instructions

- Write a command that creates a vector `x1` with elements 2,4,8,16,32,64,...,1024 without specifying explicitly the values
- Write a command that creates a vector `x2` containing the values of `x1` in the reverse order
- Replace the third and seventh value of `x2` by 10.
- Print out elements from `x2` that are greater than 150.
- Define a vector `y` with the elements of the form 150, 162,174,...,258. Let `z` be the vector of elementwise maximum of `x1` and `y`. Print out the mean value of `z`.

*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
import numpy as np
#define x1

#define x2

#modify x2

#print elements from x2 that are greater than 150

#define y

#define z

#print out the mean value of z

```

*** =solution
```{python}
import numpy as np
#define x1
x1=2**np.arange(1,11)
#define x2
x2=x1[::-1]
#modify x2
x2[np.array([2,6])]=10
#print elements from x2 that are greater than 150
print(x2[x2>150])
#define y
y=np.arange(150,259,12)
#define z
z=np.maximum(x1,y)
#print out the mean value of z
print(np.mean(z))

```

*** =sct
```{python}
import numpy as np
set_converter(key = "numpy.ndarray", fundef = lambda x: np.round(x,10))
Ex().check_object('x1').has_equal_value()
Ex().check_object('x2').has_equal_value()
Ex().check_object('y').has_equal_value()
Ex().check_object('z').has_equal_value()
test_output_contains("1024.*512", no_output_msg="the first print command should produce array with values 1024,512")
test_output_contains("307.2",pattern=False)
success_msg("Correct solution!")

```
