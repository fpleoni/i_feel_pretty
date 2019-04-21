# Please review your latest purchase!

*A look at Sephora's star rating system*

I believe deep down scraping Sephora's website has always been a dream of mine. So for this project, I decided it was time to make that dream come true.

The motivation for the project is to practice Linear Regression modeling, through the analysis of different features in order to answer an initial research question.

## Documents on this Repository

  - **src** Jupyter notebooks containing all the source code that made this analysis possible
  - **data** CSV files containing the scraped raw data, as well as the cleaned data imported from a Pandas DataFrame
  - **README.md** Description of the project, its motivations, and conclusions

## Overview

Let's break the project down into its fundamental parts:

  - Quick summary of US Beauty Industry, and the role of reviews in this context
  - The Question
  - The Data
  - Exploratory Data Analysis
  - Linear Regression
  - Conclusions
 
## US Beauty Market

The Beauty Retail Market in the US is worth $56 Billion. According to the Nielsen Future of Beauty Report (2018), the beauty market is guided by trends, both macro and micro. And the time of writing, these trens are **Clean Products**, **Transparency**, **Interconnected User Experiences**, and **Cultural Awareness**. 

So, what role does Sephora play in all this? Well, Sephora is onw of the two main players in the Beauty Retail Market (the other one being Ulta), and it is the lead beauty retailer in online sales. This leadership can be explained by the incredible investment they've made in creating a tech beauty brand, making the online experience as good as the brick-and-mortar one.

But we still haven't answer the question that steered this whole project: *What is the role of reviews?*. Well, as consumers incresingly demand transparency, reviews have become more important. Sephora went one step further by making the experience of leaving reviews similar to that of recommending a product to a friend; and by initially rewarding customers for leaving reviews (though this is long gone by now).

The problem with the importance of reviews, if that they became so influential on purchases that it created a space for less than pure motivations. In fact, there have been a few scandals in the last year involving Sephora and the reliability of the reviews on their website. But that doesn't concern this project, **much**.

## The Question

In light of what we discussed above I set sail to answer the following question: **Can we predict the review score of a product?**

**Features**
  - Price
  - Number of reviews
  - Number of loves
  - Clean (or not)
  - Category
  - Reviews to loves ration (engineered feature)
  - Price per ounce (engineered feature)
  
  **Target Variable**
    - Review score

## The Data

As mentioned earlier, for this project I got my data by scraping Sephora's website. The code for which can be found under **src/Webscraping**. From this activity I was able to put together a Pandas DataFrame containing my predictor variables and my target variable. 

Once the data was cleaned, and I had dropped all the observations that could potentially throw off the analysis, I proceeded to convert the category column into dummy variables.

## Exploratory Data Analysis

With the data clean and ready to be explored, I made some visualizations to get to know my data better, and to understand relationships (if any) between my variables.

Most Popular Brand By Reviews                               |  Most Popular Brand By Number of Products
:----------------------------------------------------------:|:------------------------------------------------------------:
![]![Most Popular Brand By Reviews](../master/images/Most_popular_by_review.png) |  ![](../master/images/Most_popular_by_number_of_products.png)

Once I had some nice plots of my data, I went ahead witha pairplot. That way I could visualize all relationships at once and decide my next steps from there.

![Pairplot](../master/images/pairplot.png)

The **key** takeaway here is that there are no linear relationships between any of the features and my target variables. The next step was to create a correlation matrix and take a look at the correlation coefficients and check for multicollinearity (though at this point I was conviced that multicollinearity was not going to be a problem, if anything, quite the opposite).

![Correlation](../master/images/correlation_matrix.png)

As we can see, as expected, there are no significant correlation between **ANY** of the variables.

At this point I was starting to feel that this was going to be an exercise in futility, but no significant findings was a valid answer to my question, so I carried on to the regression protion of the project.

## Linear Regression

Before diving into multiple linear regression, I thought it would be a good exercise to do individual regressions between the numerical continuous variables and the target variable. The results were, *not impressive*, but again, they gave me a good idea of what my next steps should be. Below you can see the results of the most extreme ones.

Linear Regression - Number of Loves                         |  Linear Regresssion - Number of Reviews
:----------------------------------------------------------:|:------------------------------------------------------------:
![Linear Regression](../master/images/lin_reg_n_loves.png)  |  ![Linear Regression](../master/images/lin_reg_n_reviews.png)



As I said, not very impressive. But still, let's take a minute and think about what the data is telling us. 

Our R-Squared is saying that 0% of the variability in our target variable (Review Score) is explained by our predictor variable (Number of Loves).

The p-value is quite high, which tells us that at a significance level alpha of 0.05 our variables have no correlation, and we fail to reject the null hypothesis.

The coefficient is very **very** small, infinitely approaching 0. A perfect 0 coefficient means that there is **NO** linear relationship whatsoever between our two variables - A change in one does not produce a change in the other.

With these results in my hands, and considering that some of the relationships in the pairplot looked like quadratic relationships (namely *Revie Score & Number of Reviews, Review Score & Number of Loves, and Review Score & Price*), I decided to go ahead with a **Polynomial Regression**. 

There were three polynomial regressions, but only two yielded results worth reporting: *Number of Loves Vs. Review Score* and *Number of Reviews Vs. Review Score*.

**Number of Loves Vs. Review Score**    |  **Residuals Plot**
:--------------------------------------:|:------------------------------------------------------------:
![](../master/images/poly_n_loves.png)  |  ![](../master/images/residuals_n_loves.png)

**Number of Reviews Vs. Review Score**    |  **Residuals Plot**
:----------------------------------------:|:------------------------------------------------------------:
![](../master/images/poly_n_reviews.png)  |  ![](../master/images/residuals_n_reviews.png)

The thing to notice here is the **residuals** plot. As you can see, both present heteroscedasticity - meaning that the variability of the error terms is not equal along the line, rather it presents as a cone shape.

Since I was still not getting ideal results, I decided to try a log transformation on my three main numerical variables (Price, Number of Reviews, and Number of Loves). Below are how the distributiones looked after the transformations.


**Price**                                    |**Reviews**                                    |**Loves**
:-------------------------------------------:|:---------------------------------------------:|:------------------------------:
![](../master/images/log_transform_price.png)|![](../master/images/log_transform_reviews.png)|![](../master/images/log_transform_loves.png)

That's better!

Now let's look at the results of the first multiple regression, and its corresponding residuals plot.

**Coefficients, Intercept, and R- Sqaured**                      |**RMSE**
:---------------------------------------------------------------:|:---------------------------------------------------------:
![](../master/images/sklearn_ling_reg_all.png)                   |  ![](../master/images/RMSE.png)

According to this particular model, oly 11.34% of the variability in **Review Score** (target variable) can be explained by our features. As you can see most of the coefficients are very close to zero, meaning they have very little effect in our target variable.

The Root Mean Squared Error value indicates the model cannot very accurately predict the target variable. Let's take a look at the residuals plot.

![Residuals](../master/images/residuals_sklearn_multi_reg.png)  

At least in this case our residuals are more evenly distributed, or homoscedastic.

At this point I was running out of things to try, but I decided to create two interaction terms and analyze their effect on the model. 

I first built a **baseline model** that had a score of **0.01026**.

The first interaction term was calculated between **Price and Clean (or not)**.

**Interaction Plot**                               |  **Model Summary**
:-------------------------------------------------:|:------------------------------------------------------------:
![](../master/images/price_clean_interaction.png)  |  ![](../master/images/clean_price_interact.png)

The Interaction plot shows there is a slight interaction interaction between the Clean(or not) feature and Price.

As we can see from the model summary though, with coefficients this low and close to zero, the relationship between our dependent and independent variables is not very significant. The R-Squared is slightly higher than what I had see thus far, but so where the p-values.

The second interaction term was calculated between **Number of Loves and Moisturizer (or not)**. 

**Interaction Plot**                                       |  **Model Summary**
:---------------------------------------------------------:|:------------------------------------------------------------:
![](../master/images/n_loves_moisturizer_interaction.png)  |  ![](../master/images/love_moisturizer_interact.png)

This model performed slightly better than the first one (R-Squared wise), but as you can see the p-values where even higher.

I tried a few more multiple regression models before getting to my last one, removing the variables with the highest p-values at each iteration. Below are the results summary and residuals plot for the last model.

**Model Summary**                                          |  **Residuals Plot**
:---------------------------------------------------------:|:------------------------------------------------------------:
![](../master/images/lin_reg_final.png)                    |  ![](../master/images/lin_reg_final_residuals.png)

As you can see, not much better. Coefficients are still very very low, and according to the R-Squares, only **10.4%** of the variability in Review Score can be explained by the independent variables. The only improvement being than only two of the p-values are higher than the significance level **alpha = 0.05**.

## Conclusions

After thorough analysis, I can say with confidence that we can't predict Review Scores, at least with the features selected or with a linear model.

That said, I don't believe the Review Scores are random, there are underlying causes at play that can't be seen through the lens of the chosen features, such as fake reviews, or paid reviews.

