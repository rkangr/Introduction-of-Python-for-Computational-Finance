---
title       : 
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:14e58130b3
## A really bad movie

Have a look at the plot that showed up in the viewer to the right. Which type of movie has the worst rating assigned to it?

*** =instructions
- Adventure
- Action
- Animation
- Comedy

*** =hint
Have a look at the plot. Which color does the point with the lowest rating have?

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

library(ggplot2)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

--- type:NormalExercise lang:python xp:100 skills:1 key:5aa8141180
## More movies

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

*** =instructions
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

*** =hint
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

*** =pre_exercise_code
```{python}
import scipy as sp
```

*** =sample_code
```{python}
# write your code here
# scipy package commands are available in the form sp.command
# define an array x with elements 1,2,3,4



```

*** =solution
```{python}
# write your code here
# scipy package commands are available in the form sp.command
# define an array x with elements 1,2,3,4
x=sp.arange(1,5)
```

*** =sct
```{python}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("sp.arange", args = "start",
              not_called_msg = "You didn't call `arange()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")


test_error()

success_msg("Good work!")
```
