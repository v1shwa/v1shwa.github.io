---
title: Understanding the math behind Linear Regression
layout: post
tags: [machine-learning, rawml]
author: Vishwa
description: Basics and Implementation of Linear Regression in Python
---

## Inside the Post 
{: .no_toc}
- TOC
{:toc}

## Introduction

Linear regression is an almost [200 year old](https://en.wikipedia.org/wiki/Regression_analysis#History) simple but one of most useful statistical models. It is used to analyze the relationship between two or more continous variables in a dataset.

The goal of this article is to understand what linear regression is & all the math that powers the model.

## What is Linear Regression

Linear Regression is a statistical method that attempts to model a relationship between two or more variables by fitting a *line* along the observed data. This *line* is called as the **regression line**.

As for every linear equation, the equation for the regression line can be written as,

$$y = b_0 + b_1X$$

where,  

- $$y$$ is called as the **dependent** or **output/target** variable,
- $$X$$ is called as **independent** variable or **predictor** or **input** variable,
- $$b_0, b_1$$ are the unknown constants called as *Y-intercept* and *slope* respectively, which we'll have to estimate.

**<u>Note</u>**: If we have more than 1 predictors in the model, then this would be called **Multiple Linear Regression** and it's equation would be like this, 

​   $$y = b_0 + b_1X_1 + b_2X_2 + b_3X_3 + ...$$

## The Perfect Regression Line

![](https://i.imgur.com/qlc2Hu4.png)

In practical world, it's nearly impossible to find the ideal regression line that covers all the data points (see picture above). So, instead, what we do is, identify the best equation that covers all the points with least errors . We call this line, the **best fitting line**.

To calculate the error, we take the sum of difference between the *estimated target values $$(\hat{y_i})$$* and *actual target values$$(y_i)$$* for all points in the dataset. To normalize the negative errors, we'll consider the squares of the errors. Now, we can formulate the error as,

​               $$ Error(E) = \sum(\hat{y_i}-y_i)^2$$

This technique is called the **Least Squares technique**. 

By the definition of linear regression, we can replace the $$y_i$$ with $$b_0 + b_1X_i$$,

​               $$E = \sum(\hat{y_i} - (b_0 + b_1X_i))$$

​                   *or*

​               $$E =  \sum(\hat{y_i} - b_0 - b_1X_i)$$

Now, our  immediate aim is to identify the ideal values for the parameters $$b_0$$ and  $$b_1$$, such that the value of *Error* function is minimized as much as possible. Let's derive that.

## Derivation of Least squares estimates

What's the first thing that comes to our mind when someone says maxima/minima of a function? — you guessed it — *Partial Derivates*.

To find the relative minima of a function, let's take the derivate of *Error function* on both the parameters $$b_0$$ & $$b_1$$ and equate them to zero.

*Note: For the sake of simplicity, I'll represent the $$\sum_{i=1}^{n}$$ as just $$\sum$$ from hereon.*

**(i) Derivative of E on $$b_1$$:**


$$
=> \frac{\partial{E}}{\partial{b_1}} \equiv 2 \sum(y_i - b_0 - b_1X_i)(-1) = 0 \\[1cm]
=> \sum(y_i) - \sum(b_0) - \sum(b_1X_i) = 0 \\[1cm]
=>  b_0 = \frac{\sum(y_i) - b_1\sum(X_i)}{n}    \longrightarrow (i)
$$



**(ii) Derivative of E on $$b_0$$:**

$$
=> \frac{\partial{E}}{\partial{b_0}} \equiv 2 \sum(y_i - b_0 - b_1X_i)(X_i) = 0 \\[1cm]

=> \sum(X_iy_i) - b_0\sum(X_i) - b_1\sum(X_i^2) = 0 \\[1cm]

Substituting\ the\ value\ of\ b_0\ from\ (i),  \\[1cm]
=> \sum(X_iy_i) - \frac{\sum(y_i) - b_1\sum(X_i)}{n}\sum(X_i) - b_1\sum(X_i^2) = 0 \\[1cm]

Multiplying\ with\ ‘n‘\ on\ both\ sides, and\ rearranging\ things\ a\ bit,\\[1cm]

=> (n-1) \sum(X_iy_i) - (n-1)b_1\sum(X_i^2) = 0\\[1cm]

Dividing\ with\ (n-1)\ on\ both\ sides\ and\ solving\ for\ b_1,\ we\ get,\\[1cm]

 {b_1 = \frac{\sum(X_iy_i)}{\sum(X_i^2)} = \frac{\bar{xy}}{\bar{x^2}}} \\[1cm]

$$

Now, by substituting this value of $$b_1$$ in the $$(i)$$, we can get the value of $$b_0$$, 

$$
b_0 = \frac{\sum(y_i) - \frac{\sum(X_iy_i)}{\sum(X_i^2)}\sum(X_i)}{n} \\[1cm]
    
{b_0 = \frac{(\sum(X_i)\sum(y_i)) - \sum(X_iy_i)}{n \sum(X_i)} = \frac{\bar{x}\bar{y}- \bar{xy}}{n\bar{x}}}
$$

## Conclusion

Thus, the *best fitting line* in simple linear regression is $$y = b_0 + b_1X$$,  where, 
$$b_1 = \frac{\bar{xy}}{\bar{x^2}}$$ and $$b_0 = \frac{\bar{x}\bar{y}- \bar{xy}}{n\bar{x}}$$ .