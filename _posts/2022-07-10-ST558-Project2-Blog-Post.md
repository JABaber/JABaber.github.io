Project 2 Reflection
================
Josh Baber
7/10/2022

## Links to GitHub repo and page

Link to GitHub page: <https://oaktreetrail.github.io/ST558_Project2/>

Link to GitHub repo: <https://github.com/oaktreetrail/ST558_Project2>

## Big Take-Aways From the Project

This project really emphasized how straightforward it is to use the
`caret` package. It is amazing how many different kinds of models it can
fit, and the amount of options one can choose for tuning parameters,
pre-processing data, and model selection. I know there are many other R
packages out there for machine learning, but `caret` really makes the
whole process easier and I wish I knew about it sooner. Also, the render
function that makes six different, but similar, documents is really
cool. While it can be a bit finicky to do, especially with GitHub, once
it gets working it is an extremely useful tool to have and a big time
saver.

## Most Difficult Part of the Project

For me, the most difficult part was figuring out what variables to use,
and how to use them. The day columns gave me trouble, especially when
trying to figure out how we can use them in the regression models
without running into collinearity issues. We decided it was best to use
the days column as a categorical variable, because we were getting
linear dependence related errors. There were other columns that were
absolute value transformations of other variables, so we had to figure
out which variable was better to use and delete the other one.

## What Would I Do Differently on the Project?

There were quite a lot of predictor variables. Some of them I cut out
because I wasn’t sure what they meant or how they were related to the
number of shares an article gets (for example the LDA variables). I
would have liked to spend more time on the analysis and selection of
predictors, since our models did not end up doing super well with
prediction. I also would want to try other methods of selecting
predictors in the linear regression models. I thought LASSO would be
good for helping reduce prediction error, but perhaps Ridge Regression
would have been better since it doesn’t penalize the number of
predictors.
