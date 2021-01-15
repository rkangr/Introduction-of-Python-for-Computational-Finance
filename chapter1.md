---
title       : Variables and basic operators
description : Defining variables

--- type:NormalExercise lang:python xp:100 skills:2 key:bf957dc21e
## Variables

Variables are means for containing given data or computation results so that we can use them in later computations. It is a good idea to give descriptive and meaningful name for a variable so that it is easy to remember, what kind values the variable contains. There are some restrictions on variable names in Python but as long as a name starts with a letter and continues with letters, numbers and underscores, it should be OK (except some reserved words that have other meaning in Python language like if, for and so on). The variable names are case sensitive (`x` and `X` are different variables). We create a variable by assigning it a value or a result of a computation. Examples of valid definitions of variables are:

```python
Price=50.5
Player1Name="Thomas"
n=500
TotalPrice=n*Price
```

 If on the right hand side of `=` is an expression involving some computations then first the result of the right hand side is computed and after that the final value is assigned to the variable


*** =instructions

- Define variables `a1`,`A2`,`Product` with values 50, 47.86 and `a1*A2`, respectively

*** =hint
- Make sure that you type the names correctly
*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
#define a1 

#define A2

#define Product

```

*** =solution
```{python}
#define a1 
a1=50
#define A2
A2=47.86
#define Product
Product = a1*A2
```

*** =sct
```{python}
Ex().check_object('a1').has_equal_value()
Ex().check_object('A2').has_equal_value()
Ex().check_object('Product').has_equal_value()
success_msg("Correct solution!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:c61ffc66e6
## Arithmetic operators

Computational programs have to perform many mathematical computations, so we have to know how to do that in Python. Fortunately most common operations work as expected in Python 3.x

Operator |	Name	| Example |	Result
 --- | --- | --- | ---
`+` |	Addition |	`x+y`	|Sum of `x` and `y`
`-`	| Subtraction |	`x-y`	| Difference of `x` and 
`*` |	Multiplication | `x*y`	Product of `x` and `y`.
`/`	| Division	| `x/y` |	 `x` divided by `y`. 7/2 gives 3.5 
`%`  |	Modulus	| `x%y` |	Remainder of `x` divided by `y`. 17%5 gives 2
`**` |	Exponent |	`x**y` |	`x` to the power `y` ($x^y$). 2**3 gives 8
`//`	| Floor Division |	`x//y` |	largest integer that is not larger than x/y. 

It is important to remember that usual rules of arithmetic hold (exponents are computed first, multiplication and division are done before additions and subtraction, same level operations are performed from left to right) and that often it is good idea to use parentheses to guarantee that operations are done in the order we want. 

**Example**: suppose we want to compute $\frac{x}{2y}$ in Python, where $x$ and $y$ are some variables. A common mistake is to write 
`x/2*y`. 
Since division and multiplication have equal precedence, the result is computed from left to right: $x$ is divided by 2 and the result is multiplied by $y$, which is not what we want (if $x=10$ and $y=5$, the final result is 25, but should be 1). A better way is to use parentheses as follows: 
`x/(2*y)`

*** =instructions
We know that the solutions to the quadratic equation $ax^2+bx+c=0$ are given by 

$$ x_1=\frac{−b+\sqrt{b^2−4ac}}{2a} $$

and 

$$x_2=\frac{−b-\sqrt{b^2−4ac}}{2a}.$$

Define the variables `a=6,b=-1,c=-1` and `x1,x2` according to the formulas for
 $x_i,\ i=1,2$. Use the knowledge that $\sqrt{x}=x^{0.5}$ so that the answer is computed by using only arithmetic operators.

*** =hint
- Both numerator and the denominator have to be grouped by parantheses

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
#define a

#define b

#define c

#define x1

#define x2

#an example of nicely formatted output
print("the solutions of the equation are x1={} and x2={}".format(x1,x2))

```

*** =solution
```{python}
#define a
a = 6
#define b
b = -1
#define c
c = -1
#define x1
x1 = (-b+(b**2-4*a*c)**(0.5))/(2*a)
#define x2
x2 = (-b-(b**2-4*a*c)**(0.5))/(2*a)
#an example of nicely formatted output
print("The solutions of the equation are x1={} and x2={}.".format(x1,x2))
```

*** =sct
```{python}
Ex().check_object('a').has_equal_value()
Ex().check_object('b').has_equal_value()
Ex().check_object('c').has_equal_value()
Ex().check_object('x1').has_equal_value()
Ex().check_object('x2').has_equal_value()
success_msg("Correct solution!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:9982b9aa0a
## Comparison operators
It is often necessary to compare two numbers (like estimated error and desired accuracy) in order to decide what our program should do next. The comparison operators are as follows:

Operator |	Description
 --- | ---
 `==` |	is equal
`!=` | not equal
`>` | greater than
`<` |	less than
`>=` | greater than or equal to
`<=` |	less than or equal to

For two numbers the result of comparison is `True` or `False`. For example, if we define `x=2`, then the value of the expression `x>=0.5` is `True` and the value of `x<1.5` is `False`

*** =instructions
Assume that variables `a` and `b` are defined. Use the `print` command to print out the results of the required comparisons

*** =hint
- Make sure that you use two equal signs for testing the equality!

*** =pre_exercise_code
```{python}
a=7
b=5
```

*** =sample_code
```{python}
# print out the result of testing the equality of a and b

# print out the result of testing if a is less than 7*b-20

```

*** =solution
```{python}
# print out the result of testing the equality of a and b
print(a==b)

# print out the result of testing if a is less than 7*b-20
print(a<7*b-20)

```

*** =sct
```{python}
test_output_contains("False.*\n.*True",
                     pattern=True,
                     no_output_msg=None)

```

--- type:NormalExercise lang:python xp:100 skills:2 key:4a523ea7e6
## True/False values in arithmetic operations
A useful property of Python (and many other languages) is that boolean values True and False are converted to 1 and 0 in arithmetical expressions. This makes it easy to write expressions that compute different values depending on some conditions without using . Example: the expression

`x**3*(x<=0)+x**2*(x>0)`

computes $x^3$ if  $x\leq 0$ and $x^2$ if $x>0$. 

This idea can be used to define piecewise continuous functions so that they also work with arrays.

*** =instructions

Assume that `x` and `y` are variables that contain real numbers. Define variable `z` according to the formula that evaluates to $x+y$ if $x\leq y$; to zero, if $y<x\leq y+1$ and to $x-y$, if $y+1<x$ by using a single expression without using `if` command. 

*** =hint

*** =pre_exercise_code
```{python}
x=27
y=-371

```

*** =sample_code
```{python}
#define the variable z in terms of x and y

```

*** =solution
```{python}
#define the variable z in terms of x and y
z=(x+y)*(x<=y)+(x-y)*(x>y+1)
```

*** =sct
```{python}
test_student_typed("#define the variable z in terms of x and y[&xyz<>\(\)\s\*\+=01-]*$",not_typed_msg="The expression you used contains wrong symbol(s)")
Ex().check_object('z').has_equal_value()
success_msg("Correct solution!")

```
