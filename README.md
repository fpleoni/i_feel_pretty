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

![Most Popular Brand By Reviews](../master/images/Most_popular_by_review.png)

![Most Popular Brand By Number of Products](../master/images/Most_popular_by_number_of_products.png)

Once I had some nice plots of my data, I went ahead witha pairplot. That way I could visualize all relationships at once and decide my next steps from there.

![Pairplot](../master/images/pairplot.png)

The **key** takeaway here is that there are no linear relationships between any of the features and my target variables. The next step was to create a correlation matrix and take a look at the correlation coefficients and check for multicollinearity (though at this point I was conviced that multicollinearity was not going to be a problem, if anything, quite the opposite).

![Correlation](../master/images/correlation_matrix.png)

As we can see, as expected, there are no significant correlation between **ANY** of the variables.

At this point I was starting to feel that this was going to be an exercise in futility, but no significant findings was a valid answer to my question, so I carried on to the regression protion of the project.

## Linear Regression

Before diving into multiple linear regression, I thought it would be a good exercise to do individual regressions between the numerical continuous variables and the target variable. The results were, *not impressive*, but again, they gave me a good idea of what my next steps should be. Below you can see the results of the most extreme one.

![Linear Regression](../master/images/lin_reg_n_loves.png)

As I said, not very impressive. But still, let's take a minute and think about what the data is telling us. 

Our R-Squared is saying that 0% of the variability in our target variable (Review Score) is explained by our predictor variable (Number of Loves).

The p-value is quite high, which tells us that at a significance level alpha of 0.05 our variables have no correlation, and we fail to reject the null hypothesis.

The coefficient is very **very** small, infinitely approaching 0. A perfect 0 coefficient means that there is **NO** linear relationship whatsoever between our two variables - A change in one does not produce a change in the other.

With these results in my hands, and considering that some of the relationships in the pairplot looked like quadratic relationships, I decided to go ahead with a Polynomial Regression.




