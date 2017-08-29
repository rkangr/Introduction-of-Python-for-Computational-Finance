---
title       : Lists, tuples and vectors
description : Introduction to composite objects


--- type:NormalExercise lang:python xp:100 skills:2 key:d92fb4b422
## List, tuples and vectors
Often there is a need to group some values together so that each of the values can be accessed easily. For example we may want to have a variable Person that contains the first name, last name and age of a person. In Python, there are two built-in types of such variables: list and tuples. Both types can contain arbitrary elements and the main difference is that the elements of a list can be changed but the elements of a tuple can not be modified later. 

A **list** can be created by using square brackets:

`Person1=["John", "Smith",25]`

Similar **tuple** can be created by parentheses:

`Person2=("Ivan", "Ivanov",19)`

Individual elements of lists and tuples can be accessed by using their numbers (that start from 0) in square brackets: `Person1[0]` gives as "John" and `Person2[2]` gives us 19 and the age of Person1 can be changed by assigning a new value to it's third component like `Person1[2]=30`.

In numerical computations we usually want to use collections of numbers (historical stock prices, vectors, matrices) and it is very convenient if those collections behave like vectors and matrices in mathematics: we want to be able to multiply a vector by a number so that all components are multiplied with this number, add two vectors of the same length element-wise and so on. Such operations are not defined for lists and this is why for computational mathematics a new data type "array" is defined. We can use this data type after importing the package NumPy by executing the command

`import numpy as np`

The part `as np` is not required but it is useful, since it allows us to use instead of the longe name numpy a shorte name np later. From now on we always assume that command has been executed.

**Vectors**

Vectors are one-dimensional arrays of numbers or boolean values (True/False). Vectors are heavily used in computational mathematics.

Some useful ways to create vectors:

1) just list the elements of a vector within the array() command inside square brackets or join two existing vectors by `append()` command.
For example, 
`x=np.array([3.4,5])` 
creates a vector x with two elements. Recall that you can see the value of the variable x by typing x and pressing the return (or enter) key in the interpreter window or by typing the command `print(x)` in the interpreter.

The command
`y=np.append(x,7)`
creates a vector y with elements 3.4,5,7. You can use as arguments for append other commands that produce vectors, like
`z=np.append(0,np.random.randn(5))`
which produces a vector starting with 0 and then containing 5 random numbers from the standard normal distribution. NB! use the `append` command as little as possible, since growing vectors is a relatively slow operation.

2) creating a vector of constant values (zeros, ones or  some other values) with the functions zeros() and ones():
`x=np.zeros(10)`
creates a vector containing 10 zeros,
`y=np.ones(5)`
creates a vector of 5 ones,
`z=3.5*np.ones(3)`
creates a vector (3.5,3.5,3.5)

3) a vector of consecutive integers in the increasing order can be formed by the function `arange(n1,n2)`, where n1 and n2 are integers. The result is a vector having n1 as the first element, n2-1 as the last element and containing all integers between those values. For example
`x=np.arange(5,11)`
produces a vector x with elements 5,6,7,8,9,10. The command arange accepts also a third argument (that is equal to 1 by default), which is used as the increment. If the third argument is given then the first element of `arange(a,b,step)` is a, second is a+step, third is a+2*step etc,  and this stops just before we get a value that is on the other side of b than a or equal to b (so b is not included). So
`y=np.arange(3,0,-1)`
produces a vector y with elements 3,2,1.

4) There is a command np.linspace() for producing linearly spaced (meaning with constant distance between consequtive elements) vectors. The most useful form is `np.linspace(start, stop, n)`, which produces n equally spaced numbers starting from the value start and ending with value stop (so the step size is (stop-start)/(n-1)). Example
`y=np.linspace(0,1,5)`
produces a vector with values 0,0.25,0.5,0.75,1

5) by using any function that returns a vector as a result, for example
`x=np.random.rand(10)`
produces a vector of 10 uniformly distributed random variables from the interval [0,1]

*** =instructions

- Write a command that creates a vector x with elements 10,0,1.5
- Write a command that creates a vector y starting with 5 ones and then 16 twos without writing explicitly out all of the elements
- Write a command that creates a vector z with values 10,9,8,...,0
- Write a command that creates a vector u with values 1,1.1,1.2,...,3
- Write a command that creates a vector w with 101 equally spaced number between -1 and 1 (including -1 and 1).
*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
import numpy as np
#define x

#define y

#define z

#define u

#define w


```

*** =solution
```{python}
import numpy as np
#define x
x=np.array([10,0,1.5])
#define y
y=np.append(np.ones(5),2*np.ones(16))
#define z
z=np.arange(10,-1,-1)
#define u
u=np.linspace(1,3,21)
#define w
w=np.linspace(-1,1,101)

```

*** =sct
```{python}
Ex().check_object('x').has_equal_value()
Ex().check_object('y').has_equal_value()
Ex().check_object('z').has_equal_value()
Ex().check_object('u').has_equal_value()
Ex().check_object('w').has_equal_value()
success_msg("Correct solution!")
```
