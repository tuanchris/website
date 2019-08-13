---
layout: blog
title: Victoria through Airbnb data
image: https://miro.medium.com/max/1400/0*nMkXRd1n4qUFUvIP
description: >
I had a vacation recently to Victoria, an island in the British Colombia district of Canada and was blown away by the beauty of it. I set out to see what I can find from its Airbnb data.
---

## Introduction
I had a vacation recently to Victoria, an island in the British Colombia district of Canada and was blown away by the beauty of it. We stayed at an Airbnb apartment in downtown Victoria and behold the beauty of the city:

![Full-width image](https://miro.medium.com/max/1400/0*nMkXRd1n4qUFUvIP){:.lead data-width="800"}
Beautiful Victoria sunset at its habour (taken by me){:.figure}


I found out that Airbnb has put many of its data available online at Inside Airbnb including listings data for Victoria. Briefly looking at the data, it was quite obvious to me that one can tell a lot about Victoria (or any other city) by analyzing the Airbnb listings. My curiosity got the better of me (and I have some time to kill on the planes), so I set out to answer the following questions to get to know Victoria better.

A glimpse at the listings data

## Questions to be answered
What Victoria neighborhood has the most listings?
What is the most popular neighborhood according to reviews?
What is the best time of year to visit Victoria?
What amenities are the most common? Are they differ across neighborhoods?
Can we predict price of a new listing?

## Data preparation
My full code for this article can be found here on my GitHub repo. There are several issues with the downloaded dataset that we have to deal with before we can do further analysis. You can follow along the code on my Jupyter notebook for the technical part.

## Data exploration
In this project, I use 3 main files downloaded from Inside Airbnb including listings.csv, reviews.csv, and calendar.csv.
listing file contains 3,655 listings in Victoria with 106 features.
reviews file contains 138,520 reviews from May 2011 to May 2019.
calendar file contains availability for listings in Victoria from May 2019 to May 2020.
What Victoria neighborhood has the most listings?
There are 29 neighborhoods in the Airbnb data for Victoria that can be grouped to 16 neighborhood groups.

## Top 5 neighborhood by listings in Victoria
We can see beside Victoria city, other destinations like Saanich, Salt Spring island, Langford… also have high number of listings.
It looks like Saanich has the most listings of 720 and accounts for 19% of all listings in Victoria
Downtown Victoria is second in terms of listing count with 13%
What is the most popular neighborhood according to reviews?
We can use reviews of listings to measure how popular a neighborhood is. Here are my observations:
Downtown Victoria appears to be the most popular area, even though it only has 480 listings (compared to 720 listings of Saanich).
Saanich, even though has 1.5 times number of listings compared to downtown Victoria, only has 19K reviews, which indicate many listings without reviews, or lower number of review per listing.
James Bay made an appearance here even though it’s not in the top neighborhood by listing count
People are quite happy staying in Victoria with an average rating of 9.66 (I was very happy with my stay as well) . Ratings across neighborhoods is quite consistent also.

Top neighborhood by review count

## What is the best time of year to visit Victoria?
We can use the rating time to indicate across the years to see what time of year is the most popular time to visit this beautiful island. The reviews we have for Victoria is from May 2011 to May 2019. However, we will only look at data from 2016–2018, not taking into account incomplete years and early years where not much reviews was done.

June to September are the best months to visit, with 60% of yearly reviews.

August got the first place with 18K reviews, account for 17% of all reviews done year round. July follows closely accounts for 15% of yearly reviews.
Not a lot of activities in Victoria during the months from January to March as those probably are the coldest month of the year.

## What amenities are the most common?
If you plan to visit Victoria, make sure you look for a place with the following popular amenities such as wifi, heating, essentials…

## Can we predict price of a new listing?
To predict price for new listing, we can use machine learning to lean from properties of a listing (such as its location, amenities, accommodation, number of bed rooms v.v..). In this project, I have tried several different models to predict listing price and here is the result of the best model:

Feature importance for our Gradient Boosting Regressor

We can see that properties of a listing such as accommodations, no of bedrooms, bathrooms, and its location can be used to predict its price.

## Next steps
For this project, I will stop here. Please clap or share if you find my post helpful. Here are some further next steps that can be done for this project:
* Try engineering new features for our models.
* Try tuning hyperparameters of the models to improve its accuracy.
* Try answering other questions using the data.
