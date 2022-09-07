---
title: Learn SQL with the e-commerce dataset on Google BigQuery
image: https://miro.medium.com/max/1400/0*q_sJBGXWX1C7WITx
description: One of the tricky things about learning anything is getting from theoretical to practical. I’m from Vietnam, where learning how to drive is nightmarish. Seriously, look up “Vietnam traffic,” and you will know what I mean. So I know a ton of people who are licensed to drive but have never done it before outside of driving school.
---

Getting started driving for Vietnamese is hard and scary. The longer people put off driving after getting a license, the longer it will be since they last did it. After a while, they started forgetting the basics, making it ever more challenging to get started.

![](https://miro.medium.com/max/1400/0*LZ58gfrzFYU-fO_V)

Photo by [Leonie Clough](https://unsplash.com/@leoniec?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Learning SQL is pretty much the same. After you learn to write a simple statement, now what? Setting up a local database is hard, and not everyone who knows SQL can do it. Besides, working with fake data you created using Excel is no fun.

So, let’s take a “drive,” shall we?

## Setting up BigQuery sandbox

First, we should start our metaphorical car. BigQuery is a managed data warehouse by Google. Being a managed service, you don’t have to spend hours learning how to create a MySQL database locally and load data there. You can start writing SQL queries in five minutes if you have a Google account, even without a credit card.

Better yet, Google has curated hundred of real-world public datasets that you can query. From massive datasets like Wikipedia and Bitcoin to Economics data, you can find data for the industry you are interested in and start from there.

To start, you must head to this [URL](https://console.cloud.google.com/bigquery) and log in with your Google account if you haven’t done so already. Next, select your country, agree to the TOS and continue. You need to create a project to start using BigQuery sandbox, a free test environment that allows you to query up to 1 TB of data per month. Select a unique name for your project and create one.

![](https://miro.medium.com/max/1140/1*XC4MPMofKSb-ssRAU7u6_Q.png)

Create a Google Cloud project (image by author)

It should only take a moment, and congrats, you now have access to the BigQuery sandbox! Select `Add data`, `Pin a project`, `Enter project name`, and put in `bigquery-public-data`. You can see all of the 240 free public datasets under this project.

![](https://miro.medium.com/max/1400/1*ZQPdilphSMlAJn5pSTp8IQ.png)

Pinning public dataset project (Image by author)

I will not discuss how to use the BigQuery UI in this article. But if you want, check out this [article](https://cloud.google.com/bigquery/docs/quickstarts/query-public-dataset-console) or, better, this [specialization](https://www.coursera.org/specializations/from-data-to-insights-google-cloud-platform) in Coursera.

## theLook eCommerce dataset

Now that we started the car let’s get to know it. With the pinned `bigquery-public-data` project, scroll all the way down, click on `more results`, and you should be able to find `thelook_ecommerce` dataset. You can select different tables, explore that data schema, and check out the actual data with preview.

![](https://miro.medium.com/max/536/1*hpvqaQlExCu6fP9ptvF4Ag.png)

Fictitious e-commerce dataset (image by author)

This is a fictitious fashion e-commerce business called Fashionly. We have a website that customers can use to purchase our products.

A customer’s journey starts when she visits our website and signs up for an account. The information that she uses when signing up is stored in the users table, and the signup date corresponds to the customer's created date.

Once signed up, she can visit our site at any time. Every time she visits, a new event is generated in the events table. We know information such as where she is browsing our site from, and what action she took (visit, add products to cart, or purchase). We also know where she was coming from (traffic source) and what type of browser she used for the access.

When she makes a purchase, an order is created in the orders table. Timestamps on when the order was shipped, cancelled, or returned are also recorded here.

Each order can contain one or several items, recorded in the order items table. The order items table is also linked with products, where we store detailed information about our products.

We have several warehouses where we store our inventories. The inventory created date is recorded when new inventories are brought to the warehouse. The same thing happens when a product is sold.

## Now let’s use your SQL!

Imagine yourself as the owner of Fashionly, head of Finance, Products, or Operations. What would you like to know about your business? Here are some questions to get you started.

-   How much are we selling daily? Is it high or low compared to yesterday, the same time last week/month/year?
-   Who are our customers? Break down by demographics. What are their purchasing behaviours? Are they buying more or less? How fast are we signing up new customers?
-   What are we selling the most and the least? What are we making money on? Are some products/categories selling more to a particular group of customers?
-   What geographic location are we doing well/not well? Can our warehouse cover all areas? When and where should we think about expanding our fulfillment capability?
-   What marketing channel are we doing well on? What is our current mix? Is there a change in trends?

There are many, many more questions that you can ask to understand your business further and make better decisions.

Let’s walk through a couple of questions together. We will start with a basic query to find out how much we are selling, how many orders per day and how many customers purchased. To do that, we have to join orders and order\_items together. Be sure to filter out cancelled and returned orders in your query.

<script src="https://gist.github.com/tuanchris/2194a3d8012cb3f245d99ccbda570ac5.js"></script>

![](https://miro.medium.com/max/1060/1*2f3UOhA9LW84mlC596A_JQ.png)

Basic business info (image by author)

We can see that we are selling around $30–40K per day, processing around 400 orders with about 300 customers purchasing. There are some days that we sell a lot more than the average.

Next, let’s look at a slightly more complicated query. I want to know what category customers purchase the most with the first order. To do that, we would have to use a window function to identify first orders. Then we can just group by product category and calculate our revenue and user count.

<script src="https://gist.github.com/tuanchris/50ea8a472b4ce373d80d6e06dcad6e20.js"></script>

![](https://miro.medium.com/max/1006/1*4AuwMdRpPfZDf-JpfutVVg.png)

Top categories for first orders (image by author)

Now, if I want to create a campaign to drive new user acquisition, I know that Outwear would likely bring me the most revenue, whereas Jeans would bring me the most customers.

## Summing up

BigQuery is an effortless way for you to get started with learning SQL. Only by going out there and “drive”, aka applying SQL to answering real-world business problems, can one truly learn how to use this in-demand skill.

[Here](https://cloud.google.com/bigquery/docs/best-practices-costs) are some best practices when working with SQL in BigQuery that I think you should know about.

Thank you for reading, and I hope this article helps you in some way.
