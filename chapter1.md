---
title       : Insert the chapter title here
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:VideoExercise lang:r xp:50 skills:1
## Анализ рейтинга фильмов

*** =video_link
//player.vimeo.com/video/154783078

--- type:MultipleChoiceExercise lang:r xp:50 skills:1
## Реально плохое кино

Посмотрите на график, появившийся в окошке справа. Фильмы какого типа имеют худший рейтинг?
Have a look at the plot that showed up in the viewer to the right. Which type of movie has the worst rating assigned to it?

*** =instructions
- Приключения
- Экшен
- Мультфильм
- Комедия

*** =hint
Посмотрите на график. Какого цвета точки с  самым низким рейтингом?
Have a look at the plot. Which color does the point with the lowest rating have?

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace. You can use it for several things:

# 1. Preload a dataset. The code below will read the csv that is stored at the URL's location.
# The movies variable will be available in the user's console.
movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

# 2. Pre-load packages, so that users don't have to do this manually.
library(ggplot2)

# 3. Create a plot in the viewer, that students can check out while reading the exercise
ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

*** =sct
```{r}
# The sct section defines the Submission Correctness Tests (SCTs) used to
# evaluate the student's response. All functions used here are defined in the 
# testwhat R package

msg_bad <- "Неверно!"
#msg_success <- "Именно! Похоже, в этом наборе действительно много плохих экшенов."
msg_success <- "Exactly"

# Use test_mc() to grade multiple choice exercises. 
# Pass the correct option (Action, option 2 in the instructions) to correct.
# Pass the feedback messages, both positive and negative, to feedback_msgs in the appropriate order.
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad)) 
```

--- type:NormalExercise lang:r xp:100 skills:1
## Еще несколько фильмов

В предыдущем упражнении вы видели набор данных о фильмах. В этом упражнении мы посмотрим еще один набор данных о фильмах.
In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

Набор данных о фильмах `movie_selection` доступен в рабочем пространстве.
A dataset with a selection of movies, `movie_selection`, is available in the workspace.

*** =instructions
- Check out the structure of `movie_selection`. Просмотрите структуру фрейма `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`. Выберите фильмы с рейтингом от 5 и выше, резальтат сохраните во фрейме `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`. Используйте функцию `plot()` для построения графика с `good_movies$Run` по горизонтальной оси и `good_movies$Rating` по вертикальной, передайте параметру  `col` значение `good_movies$Genre`.

*** =hint
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`. 

*** =pre_exercise_code
```{r}
# Pre-load a package in the workspace
library(MindOnStats)

# You can prepare the data before the student starts:
data(Movies)
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"),c("Genre", "Rating", "Run")]

# You can also clean up data so that it's not available in the student's workspace anymore:
rm(Movies)
```

*** =sample_code
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

*** =solution
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

*** =sct
```{r}
# The sct section defines the Submission Correctness Tests (SCTs) used to
# evaluate the student's response. All functions used here are defined in the 
# testwhat R package. Documentation can also be found at github.com/datacamp/testwhat/wiki

# Test whether the function str is called with the correct argument, object
# If it is not called, print something informative
# If it is called, but called incorrectly, print something else
test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

# Test the object, good_movies
# Notice that we didn't define any feedback here, this will cause automatically 
# generated feedback to be given to the student in case of an incorrect submission
test_object("good_movies")

# Test whether the student correctly used plot()
# Again, we use the automatically generated feedback here
test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

# Alternativeley, you can use test_function() like this
# test_function("plot", args = c("x", "y", "col"))

# It's always smart to include the following line of code at the end of your SCTs
# It will check whether executing the student's code resulted in an error, 
# and if so, will cause the exercise to fail
test_error()

# Final message the student will see upon completing the exercise
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1
## Упражнение 1

Создайте переменную `a` и присвойте ей значение 3.01. Создайте переменную `b` и присвойте ей значение 3.23.

*** =instructions
- Создайте новую переменную `a` и присвойте ей значение 3.01.
- Создайте новую переменную `b` и присвойте ей значение 3.23.

*** =hint
- Используйте оператор присваивания `<-`. 

*** =pre_exercise_code
```{r}
a <- 3.01
b <- 3.23
```

*** =sample_code
```{r}
# Создаем переменную a

# Создаем переменную b

```

*** =solution
```{r}
# Создаем переменную a
a <- 3.01

# Создаем переменную b
b <- 3.23
```

*** =sct
```{r}
# Test the object, good_movies
# Notice that we didn't define any feedback here, this will cause automatically 
# generated feedback to be given to the student in case of an incorrect submission
test_object("a")
test_object("b")

test_error()

success_msg("Отлично!")
```


--- type:NormalExercise lang:r xp:100 skills:1
## Упражнение 2

Вычислите квадрат суммы значений `a` и `b` и присвойте результат переменной `d`.

*** =instructions
- Создайте новую переменную `d` и присвойте ей квадрат суммы значений `a` и `b`.

*** =hint
- Используйте оператор присваивания `<-`. 

*** =pre_exercise_code
```{r}
a <- 3.01
b <- 3.23
```

*** =sample_code
```{r}
# Создаем переменную d

```

*** =solution
```{r}
# Создаем переменную d
d <- (a+b)^2
```

*** =sct
```{r}
# Test the object, good_movies
# Notice that we didn't define any feedback here, this will cause automatically 
# generated feedback to be given to the student in case of an incorrect submission
test_object("d")

test_error()

success_msg("Отлично!")
```



--- type:NormalExercise lang:r xp:100 skills:1
## Упражнение 3

Oкруглите d до третьего знака после запятой.

*** =instructions
- Oкруглите d до третьего знака после запятой, результат присвойте той же переменной.

*** =hint
- Используйте функцию `round()` и аргумент `dec`.

*** =pre_exercise_code
```{r}
a <- 3.01
b <- 3.23
d <- (a+b)^2
```

*** =sample_code
```{r}
# Округляем d

```

*** =solution
```{r}
# Округляем d
d <- round(d, dec = 3)
```

*** =sct
```{r}
# Test the object, good_movies
# Notice that we didn't define any feedback here, this will cause automatically 
# generated feedback to be given to the student in case of an incorrect submission
test_function("round", args = "x")
test_function("round", args = "dec")

test_object("d")

test_error()

success_msg("Отлично!")
```