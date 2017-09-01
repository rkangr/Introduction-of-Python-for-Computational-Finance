---
title       : Programming basics
description : Main programming constructs in Python

--- type:NormalExercise lang:python xp:100 skills:2 key:2a7a755065
## Programming constructs
Numerical methods studied in this course are iterative in nature, meaning that they require a large number of repetitions of computations according to the same formulas and the number of repetitions required is sometimes known but sometimes is not known at the beginning but has to be determined during the computations by certain conditions. So we have to know some ways to write such code.

Fortunately this can be accomplished by a small number of programming constructs, that are outlined below.

1) Simple `if` statement works as follows:

```python 
if condition:
            command1
            command2
            .......
other commands
```

 means that the commands with indentations after the if clause are executed only if condition is True. So with 

```python
x=3
if x>1:
     print("condition was true")
     print("second command inside if")
print("outside of if, always printed")
```

three sentences are printed (since the comparison `x>1` gives True). If we change x to 10 in the first line, then only the last print command is executed, so only one line is printed.

2) We can add alternatives

```python
if condition:
          expressions1
else:
         expressions2
other commands
```

 is an extension of this, where depending on whether the condition is True or False different expressions get evaluated. So with
 
 ```python
if np.random.rand(1)>np.random.rand(1):
   print("first was bigger")
else:
   print("second was bigger or equal")
```

two random numbers from the unit interval are generated and then if the first one is larger than the second one then corresponding message is printed. However, if this is not the case then the other message is printed.

Remark: Of course the body of `if` (ie expressions1) or `else` (i.e. expressions2) may contain another if or if...else constructs.

3) Repeated computations with `for` loop:

```python
for variable in vector:
         commands
other commands executed after the for cycle is complete
```

is an example of a cycle (or loop). The basic idea is that variable takes the value of the first element of the sequence and the commands are then executed, then the variable takes the value of the second element of the sequence and expressions are again executed; this continues until the sequence is exhausted. Suppose we want to compute 100 elements of the sequence $x_i$ defined by the relations

$x_0=1$ 

and 

$x$<sub>*i*</sub> $=\frac{1}{1+{x_{i-1}}^2}.$

Consider the  code

```python
n=100
x=np.ones(n)
for i in np.arange(1,n):
   x[i] = 1.0/(1+x[i-1]**2)
```

It produces first two objects (a variable n and a vector x) and then begins a cycle. At the first step variable i gets value 1 (first value in the vector). In the body of the cycle the second element of the vector x is computed by using the known value of the first element $x$<sub>0</sub> . Now the variable i gets value 2 (second value in the vector) and in the body of the cycle the third element of the vector x is changed. This cycle continues till i=99 (last value in the vector) and in the last step the last element of the vector x (ie $x$<sub>99</sub>) is changed. Then the cycle terminates as i has received its last value. If we look at the values of x, then we see, that the sequence seems to converge to a fixed value approximately equal to 0.6823278.

Remark:  It is best not to use cycles in Python unless absolutely necessary as usually a code using vector operations instead of cycles is much faster. For current example we can not use vector operations since the values $x$<sub>1</sub>,$x$<sub>2</sub>,$\ldots$, $x$<sub>$n-1$</sub> have to be computed one at a time starting from $x_1$. Often we need to perform repeated computations that can be done independently and then vector operations make code simple and faster. For example the sum of numbers $1,\frac{1}{2^2},\frac{1}{3^2},\ldots,\frac{1}{1000^2}$ could be computed without using numpy package by a for cycle as follows (by using a standard function range that returns a list of integers):

```python
n=1000
result=0 #contains the current value of the sum
for i in range(1,n+1):
     result=result+1/i**2 #add next term to the current value
print(result) 
```

Here it is important to understand that all the terms in the sum can be computed independently of each other. So by using NumPy we can compute the vector of the terms and the use the function sum():

```python
n=1000
i=np.arange(1,n+1)
terms=1/i**2 #computes the vector of numbers we want to sum
result=np.sum(terms)
print(result)
```

This code works much faster in Python

4) While loop:

```python
while condition:
         expressions
commands executed after the while cycle ends
```

is a different kind of cycle where expressions are executed if the condition is TRUE initially; then the condition is re-checked and if it is still true then expressions are executed again; this continues until the condition is FALSE. Basically this looks very much like a for cycle presented previously but the difference is that the number of times the cycle body is run is not predetermined. Consider the previous example, but suppose we want to find the value to which the sequence xi converges with a given accuracy. If this is our aim, we do not have to store all values of xi we compute, we just need the last one and for checking the convergence also the previous one. So we can write

```python
xi_1=1
xi=1.0/(1+xi_1**2)
error=0.00000001
while np.abs(xi-xi_1)>error:
   xi_1=x_i#the last value becomes the previous one
   xi=1.0/(1+xi_1**2)
print(xi)
```

The variable `xi_1` denotes $x$<sub>$i-1$</sub>, the previous value, and `xi` stands for $x$<sub>$i$</sub>, the current (new value). We decide to continue computing until the difference between the current and previous values is small enough, for which we use the variable error. After the three variables have been defined a cycle starts. At each iteration, the difference of the current and the previous values is compared with the allowed error. If the difference is larger than the error, then the commands in the body of the while cycle are executed: the current value becomes the previous one (ie `xi_1` takes the value of `xi`) and a new value of `xi` is computed. If the difference is smaller than the error, the while cycle ends and the next command outside the cycle is executed (in this case the print command).

Typically constructs presented are combined -- e.g. the body of a `for` cycle may contain an `if` construct, another `for` or `while` cycle and so on.

*** =instructions

- The basic iteration method for solving equations of the form $x=f(x)$ is given by $x$<sub>$i+1$</sub>=$f(x$<sub>$i$</sub>$),\ i=0,1,\ldots$, where $x$<sub>0</sub> is a given initial approximation to the solution. Write a function `BasicIter` with three arguments `n,x0` and `f`, which outputs a vector of values $x$<sub>0</sub>,$x$<sub>1</sub>,...,$x$<sub>$n$</sub> computed according to the iteration method with $x$<sub>0</sub>=`x0` (the given value). Output the results for `x0=0, n=5`, when the function `f` is defined according to the formula $f(x)=\sin(x)+0.5$ (so we solve approximately the equation $x=\sin(x)+0.5$)
- Write a function `BasicIter2`, which instead of `n` takes a given error as the first argument and outputs the first value of $x$<sub>$i$</sub>, for which the the difference |$x$<sub>$i$</sub>-$x$<sub>$i-1$</sub>| is less than the given error together wiht the value of $i$ (the number of iterations) that was needed. Use it to solve approximately equation $x=\cos(x)-0.3$. with $x$<sub>0</sub>=0 and error 0.001. 

*** =hint


*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
# import numpy 

# define the function BasicIter

# define f (can use a different name of the function)

#output with print command the result corresponding to given parameters

#define Basiciter2

#define a function corresponding to the expression cos(x)-0.3

#print out the result of solving the equation x=cos(x)-0.3 obtained by Basiciter2


```

*** =solution
```{python}
import numpy as np
def BasicIter(n,x0,f):
     x=x0*np.ones(n+1)#we need n+1 elements to get x0,...,xn
     for i in range(0,n): #the last value of i is n-1
         x[i+1]=f(x[i])
     return(x)
#define the function of the example
def f1(x):
     return(np.sin(x)+0.5)
#output the result
print(BasicIter(5,0,f1))

#assume the previous code has been executed, so f1 is defined
def BasicIter2(error,x0,f):
    xi=0
    xip1=f(xi) #denotes the value of x with index i+1
    i=1
    while np.abs(xip1-xi)>error:
       xi=xip1
       xip1=f(xi)
       i=i+1
    return(np.array([xip1,i]))
def f2(x):
   return(np.cos(x)-0.3)
print(BasicIter2(0.001,0,f2))
```

*** =sct
```{python}
test_output_contains("0.*0\.5.*0\.979.*1\.495", no_output_msg="the first print command should produce six numbers starting from 0 and ending with 1.49504345")
test_output_contains("0.5519026.*11",no_output_msg="the second print command should produce firts the value 0.5519026 and then the number of iterations, which is 11")
success_msg("Correct solution!")

```
