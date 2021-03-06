---
layout: post
title: Can College Rankings Predict Return On Investment?
---

### The case of college ROI

Going to college is  one of the most important decisions in life. As a parent, I was interested in finding out what might  predict the return on this investment.

The first thought came to mind was college rankings. After all, if a college ranks high, wouldn't it suggest students receive better eduction and thus likely to earn more after graduation? 

The cost, of course is a must in calculating  ROI since we are considering net profit so to speak. Last, I wanted to bring endowment into the equation because not only does it help cover school and student's expenses but also it's a good indicator of how well off the alums are and how much they value their experience at their alma mater.

Having made up the hypothesis, it was time to test it with data science.

For rankings, there are many sources, including prominent ones such as US news and Forbes. I ultimately decided to go with [niche.com](https://www.niche.com/colleges/search/best-value-colleges/) because it is free and has the largest number of schools (2000+) and ranking categories (dozens, including overall, academics, athletics, student life, political leaning, etc.).

For ROI, there isn't a perfect source. The best available and most widely used is from [payscale.com](https://www.payscale.com/college-roi), despite its flaws such as selection bias as data is self reported by users or that 4 year completion rate is not accounted for. So this is where I got ROI information.

As to endowment, I chose [endowments.com](http://endowments.com/) for it has the most extensive list of schools (800+). 

After cleaning data from each source, I then joined them by school name in one table. By examining the characteristics of each column, I decided to try three different data transformations to see which would work best for modeling.

* Transformation #1. Convert school rankings to bins.
* Transformation #2. Convert school rankings to exponential decay
* Transformation #3. Convert school rankings to z scores.


Once data preparation was done, I started the model selection process. The metric I used was MAE(mean absolute error) for best intepretability. I experimented with linear and quadratic ridge and lasso regression, using grid search CV function from Sci kit-Learn to optimize tuning parameter alpha. The model that got the best score was linear lasso regression with alpha = 0.05 on data transformations #3, so that was my final selection.

When evaluating the final model, I examined the risiduals vs.prediction plot. The plot showed a clear linear trend, indicating some variation in target (roi) was not explained by the model and instead 'leaked' into the residuals. In fact, in another plot of prediction vs. mean, I found that the prediction was not much better than just predicting the mean.

__In other words, the combined information of college rankings, cost and endowment is not sufficient for ROI forecast.__

So, What's the main takeaway from my investigation?

__Don't base college decision on rankings if your goal is to maximize ROI!__

Will I keep pondering about this question? You bet! But next time, I will try adding new features like college majors or using different models to see if better prediction can be achieved.

