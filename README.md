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

Once the data was cleaned, and I had dropped all the observations that could potentially throw off the analysis, I proceeded to convert the category column into dummy variables. Please see the picture below:


