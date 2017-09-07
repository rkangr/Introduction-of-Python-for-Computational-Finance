---
title       : Functions
description : Defining functions in Python


--- type:NormalExercise lang:python xp:100 skills:2 key:70413ba714
## Functions
it will be very useful to write several functions of your own. Well-defined functions make our code easier to read and to modify. Whenever there is a need to use similar pieces of code over and over again, it is a good idea to define a corresponding function instead.

How do we define a function?
Typically with a command similar to this

```python
def=function_name(arguments):
    first command
    second command
    ...
    last command (usually return(value))
first command outside of the function
```

So a function really is comprised of three parts: it's name, it's arguments and the function body (this is the main part that starts at the next line after :  and should be indented (ie placed in some distance from the left margin, each command at the same distance). Usually it is good idea to write the code of a function in the editor window and then execute either the full file or, if the IDE allows it, a part of it. In the Spyder IDE you can execute a selected part of code by pressing F9.

Let us consider some examples. 

First, suppose we want to do various computations with the function $$f(x)=x^3-3x+2$$. It is clear that this function should have one argument x and that it should return the result of computing $$x^3-3x+2$$ for a given value of x. So we can define

```python
def f(x):
    return(x**3-3*x+2)
```

After executing the definition in the interpreter, we can use the function in several ways. For example, we can compute it's value at x=3 by typing
f(3)
in the interpreter (and should see the result 20). Even better, since when using the package NumPy all usual commands work elementwise on vectors, we can compute several values of the function f just by giving a vector of x-values as the argument as follows:

```python
x_values=np.linspace(0,1,101)
f_values=f(x_values)
```

Now the vector f_values contains 101 numbers corresponding to f(0), f(0.01), f(0.02),...,f(1). So we can easily produce the graph of the function f by using the functions plot and show form the package pylab:

```python
import pylab as pl
pl.plot(x_values,f_values)
pl.show()
```

After executing the last command a new window containing the graph of the function should appear.

Next, let us consider the example of finding solutions of quadratic equations $$a\,x^2+b\,x+c=0$$. Let us assume for simplicity that a is not equal to 0. The most obvious way is to define a function of three variables a, b, c that returns a vector of two (possibly equal) solutions as follows:

```python
def quad_solver1(a,b,c):
    D=np.sqrt(b**2-4*a*c)
    result=np.zeros(2)
    result[0]=(-b-D)/(2*a)
    result[1]=(-b+D)/(2*a)
    return(result)
```

Note that we defined new variables D and result inside the function. These variables are local to the function. This means that the values of the variables disappear as soon as the function returns it's result and can not be seen outside of the function. If we have variables with names D and result defined also outside the function, the values of the outside variables are not affected when the function quad_solver1 is executed.

If we want to solve $$x^2-x-6=0$$ we can now simply type
`quad_solver1(1,-1,-6)`
in the interpreter window (and should see the answer [-2,3]).

Sometimes it is more convenient to think that a quadratic equation is represented by a vector of its coefficients and so we may want to use a solver which takes the vector of coefficients as its argument. When writing the function, let us denote by x the vector containing the values of the coefficients a,b,c. If we want to have both versions of solvers available, we can use quad_solver1 inside the new function quad_solver2:

```python
def quad_solver2(x):
    return quad_solver1(x[0],x[1],x[2])
```

But if we want that the second solver works without the need of defining the first one, we can modify the code of the second solver as follows:

```python
def quad_solver2(x):
    a=x[0]
    b=x[1]
    c=x[2]
    D=np.sqrt(b**2-4*a*c)
    result=np.zeros(2)
    result[0]=(-b-D)/(2*a)
    result[1]=(-b+D)/(2*a)
    return(result)
```

Now we have to keep in mind that the argument given to quad_solver2 should be a vector of three coefficients. So we can write

```python
eqn=np.array([1,-1,-6])
print(quad_solver2(eqn))
```

to solve the previously given equation. Note that our solver works also when a list or a tuple is used instead of a vector (so we could have defined eqn=(1,-1,-6) in the previous example).

As we saw it is up to us to decide in what form the necessary data should be given to a function when we define a function but when using a function, we have to give the data to it exactly in the form it expects.

The arguments of a function can be of any type: they can be numbers, vectors, matrices, names of other functions etc. In computational finance it is often useful to define functions that take a name of another function as an argument.  Consider the following example.

Suppose we often need to find approximately the maximal value of various functions of one variable over various intervals.  If we do not need a very high accuracy we can find the maximal value just by computing the function values at sufficiently many equally spaced points in the given interval. So let us write a function maxval with the following arguments: the name of the function we are interested in, the starting point of the interval, the endpoint of the interval and the number of points used.

```python
def maxval(f,start,end,n=100):
    points=np.linspace(start,end,n)
    result=np.max(f(points))
    return(result)
```

Now when we use the function maxval, we should write for the first argument a name (without parentheses and arguments) of any function of one variable that works correctly when the variable is a numeric vector. Since the last variable n is given a default value 100, we can give only 3 arguments for the function if we think that computing the values at 100 points is enough. For example we can use the standard mathematical functions defined in NumPy package:

`maxval(np.cos,1,5)`

computes approximately the maximal value of the function cos(x) for x in the interval [1,5]. We can also use the names of functions we have defined ourselves:

```python
def g(x):
    return(x*np.sin(x))
print(maxval(g,0,6,1001))
```

It is important to understand that after an argument with a default value there should be no other arguments without default values. So if we want to give a default value for the argument start, we should also give default values for the arguments end and n.

*** =instructions
- Write a function Bounds that gets a vector of numbers as an input and returns the two dimensional vector containing the minimal and the maximal values of the given vector as the output.
- Write a function average_f, that takes as arguments the name of a function of one variable and an integer n and returns the arithmetic average of the values of the function at argument values 1,2,...,n. Test your function with the sine and cosine functions for n=1000.

*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
#import the NumPy package with the name np

#define the function Bounds

#define the function average_f


```

*** =solution
```{python}
#imort the NumPy package with the name np
import numpy as np
#define the function Bounds
def Bounds(x):
    return(np.array([np.amin(x),np.amax(x)]))
    
#define the function average_f
def average_f(f,n):
    x=np.arange(1,n+1)
    return(np.mean(f(x)))

```

*** =sct
```{python}
Ex().has_equal_value(expr_code="Bounds(np.array([0,-1.1,3.14]))")
Ex().has_equal_value(expr_code="average_f(np.sin,10)")
success_msg("Good job!")
```
---
title       : Functions
description : Introduction to the syntax for defining functions
Almost every command that we use in Python makes use of a function.  You have already seen many useful functions that are predefined and many others are available in different packages. However, throughout the course 
