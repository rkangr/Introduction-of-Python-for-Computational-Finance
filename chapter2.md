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

 If on the right hand side of `=` is an expression involving some computations then first the result of the right hand side is computed and the final value is assigned to the variable


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
## Basin operators
Arithmetic operators

In Computational Finance course our programs have to perform many mathematical computations, so we have to know how to do that in Python. Fortunately most common operations work as expected in Python 3.x

Operator |	Name	| Example |	Result
--- | --- | --- | ---
`+` |	Addition |	`x+y`	|Sum of `x` and `y`
`-`	| Subtraction |	`x-y`	| Difference of `x` and 
`*` |	Multiplication | `x*y`	Product of `x` and `y`.
/	| Division	| x/y |	Quotient of x and y. 7/2 gives 3.5 
%  |	Modulus	| x%y |	Remainder of x divided by y. 17%5 gives 2
** |	Exponent |	x**y |	x to the power y ($x^y$). 2**3 gives 8
//	| Floor Division |	x//y |	gives largest integer that is not larger than x/y. 


*** =instructions

*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}

```

*** =solution
```{python}

```

*** =sct
```{python}

```
