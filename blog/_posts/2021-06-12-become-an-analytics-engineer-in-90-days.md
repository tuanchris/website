---
title: Become an Analytics Engineer in 90 days
image: https://miro.medium.com/max/4000/0*NZTmCXAX3WgMX_pT.png
description: The tale of a Data Analyst who evolves into an Analytics Engineer and resources so you can use to be like her.
---
# Become an Analytics Engineer in 90 Days

Analytics Engineer is a new position [coined](https://www.getdbt.com/what-is-analytics-engineering/) (and made possible) by dbt. If a Data Engineer (DE) marries a Data Analyst (DA) and they have a baby girl, that baby girl will be an Analytics Engineer (AE). Well, it does not work that way, but you get the point.

![[Image Credit](https://www.getdbt.com/what-is-analytics-engineering/)](https://cdn-images-1.medium.com/max/2260/1*qnVbe-WCi147h0mKxk10jQ.png)*[Image Credit](https://www.getdbt.com/what-is-analytics-engineering/)*

## The context

An AE often starts off as a DA creating dashboards and doing ad-hoc queries. She wants to do more because that DE guy works like a snail. She knows her data well because she spent hours per day navigating it using her mad SQL skill. She also knows the business inside out, having to interact with them on a daily basis. But she is faced with enormous challenges wanting to take on the work of the DE guy. Here are some of them:

* The pipelines were built in Python, and she doesn’t know how to code (besides SQL).

* The DE guy mentioned something about using git to keep track of changes in the source code. She has her SQL codes stored in word files…

* She has very little knowledge about the systems that produce data.

* The team is using all sorts of tools, and she’s not familiar with them all.

* That DE guy thinks this is above her, which pissed her off even more.

## The solution

If only our DA gal can do the work that the arrogant DE does without becoming him… Enter [dbt](http://getdbt.com) (data build tool)! How can a tool like this create an entirely new position in the field, you ask? Let’s see.

* She can write transformation code with SQL instead of Python. What?

* She can test for duplications in joins statements programmatically. Really?

* She can write data documentation so that business people will bother her less. Nice!

* She can use for loop and variable, pivot data using SQL templating. Splendid!

* She can show data lineage, so people know where data is coming from and what has been done with it. Awesome!

![[Image credit](https://blog.ml6.eu/trends-analytic-engineering-with-dbt-or-dataform-252afc8864ec)](https://cdn-images-1.medium.com/max/3200/1*eYG4ePicO1UGTruOUr3yhQ.png)*[Image credit](https://blog.ml6.eu/trends-analytic-engineering-with-dbt-or-dataform-252afc8864ec)*

## The evolution

And just like that, our DA gal evolves into an AE.

![[Image credit](http://www.gamersheroes.com/game-guides/how-to-evolve-pikachu-in-pokemon-sword-shield/)](https://cdn-images-1.medium.com/max/2000/0*ZBgFKyScPNTUA6EK)
*[Image credit](http://www.gamersheroes.com/game-guides/how-to-evolve-pikachu-in-pokemon-sword-shield/)*

I’m kidding. It does not work like that. It takes time, effort, and commitment to learning new stuff. If you can relate to the story of our DA girl, I think this article will benefit you.

Here is an opinionated list of skills/technologies **I think** are necessary to become an AE ninja.

* **SQL ninja:** If you are a soldier, then SQL is like your weapon. SQL has become the standard for data extraction and transformation. As an AE or a DA, you must get as comfortable with SQL as possible.

* **Git warrior**: Git is a powerful tool for collaboration in a team. You are expected to wield this weapon like an extension of your arm.

* **dbt guru:** dbt is the technology that enables AE and DA to do the work of DE. With dbt, you can easily participate in the previously DE-only work and do a lot with data.

* **BI tools expert**: Dashboard is not only numbers and graphs; it is a powerful tool to tell a story.

* **Cloud champion**: Cloud computing is one of the reasons we have the 4th industrial revolution. Becoming a cloud champion can only help with your career progression.

* **Scrum master**: Scrum is a framework utilizing an agile mindset for developing, delivering, and sustaining complex projects.

* **Documentation advocate**: We, as the human race, only got this far thanks to collective learning. Writing is a potent tool of communication, and you will benefit tremendously from practicing it.

## The resources

Below are the resources that we use at [Joon Solutions](http://joonsolutions.com) to onboard our new Analytics Engineer. It works better as a checklist, so perhaps you can copy these to your favorite note-taking app.

I can’t guarantee that by following this, you will be an AE. But I’m sure that you can learn a lot following this path, and with the right environment and team, you will evolve to an **Analytics Engineer ninja**.

Happy learning!

### I have become a **SQL Ninja**

* I have taken the [W3School SQL](https://www.w3schools.com/sql/) course

* I have taken the [SQLBolt](https://sqlbolt.com/) course

* I have gone through the [BigQuery syntax doc](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) and asked all the questions I need to

* I have explored at least one [BigQuery public dataset](https://cloud.google.com/bigquery/public-data) and made some cool-ass queries.

* I know what [window functions](https://mode.com/sql-tutorial/sql-window-functions/) are and how to use them

* I have checked out additional resources such as [this](https://towardsdatascience.com/6-of-the-best-niche-platforms-to-learn-sql-and-python-f6f13808d2f5), [this](https://towardsdatascience.com/learning-sql-learn-how-to-practice-sql-with-a-complex-database-4b2ce933b1ef), and [this](https://websitesetup.org/sql-cheat-sheet/)

* I admit that [SQL is powerful](https://medium.com/dataform/consider-sql-when-writing-your-next-processing-pipeline-5167f67afb16)

### I have become a **Git warrior**

* I know what [git](https://www.atlassian.com/git/tutorials/what-is-git) is

* I know what a typical [git workflow](https://www.atlassian.com/git/tutorials/comparing-workflows) looks like

* I have created a test repo, a commit, and submit a pull request

* I know what an SSH key is, where to find it, and how to [add it to my GitHub account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

* I have checked out cool resources like [this](https://guides.github.com/), [this](https://www.atlassian.com/git), and [this](https://medium.com/cs-code/beginners-guide-to-using-git-8e5001791fa6)

### I have become a **dbt guru**

* I know [what dbt is](https://blog.getdbt.com/what--exactly--is-dbt-/#:~:text=dbt%20(data%20build%20tool)%20is,Casper%2C%20Seatgeek%2C%20and%20Wistia.) and why it’s powerful

* I have read the [analytics engineer guide](https://www.getdbt.com/analytics-engineering/)

* I have taken the dbt [on-demand course](https://courses.getdbt.com/collections)

* I have set up a dbt project from scratch and built some awesome models

* I have read through and understood the [dbt project checklist](https://discourse.getdbt.com/t/your-essential-dbt-project-checklist/1377)

* I have read through and understood the [dbt best practices](https://docs.getdbt.com/docs/guides/best-practices)

* I have read through and understood [dbt coding convention](https://github.com/fishtown-analytics/corp/blob/master/dbt_style_guide.md)

* I am ready and excited to build real projects with dbt

### I have become a **BI tool expert**

* I have looked at the BI tools landscape and know what’s out there

* I have read the [Storytelling with data](http://www.bdbanalytics.ir/media/1123/storytelling-with-data-cole-nussbaumer-knaflic.pdf) book

* I have read the [Analytics Setup Guidebook](https://www.holistics.io/books/setup-analytics/)

* I have tried out and built a dashboard with [Power BI](https://powerbi.microsoft.com/en-us/)

* I have tried out and built a dashboard with [Metabase](https://www.metabase.com/)

* I have tried out and built a dashboard with [Holistics](https://www.holistics.io/)

* I have tried out and built a dashboard with [Data Studio](https://datastudio.google.com/u/0/navigation/reporting)

* I can say with confidence that I know what BI tool is right for different needs

### I have become a **Cloud champion**

* I knew about the [many services](https://cloud.google.com/products/) of a major cloud provider

* I knew about the [many benefits](https://www.softwareadvisoryservice.com/en/blog/why-move-to-the-cloud-12-benefits-of-cloud-computing-in-2019/) of using the cloud

* I have tried creating a BigQuery dataset and [loaded data](https://cloud.google.com/bigquery/docs/loading-data) in

* I have tried out [BigQuery ML](https://cloud.google.com/bigquery-ml/docs) and knew how easy it is to create an ML model with SQL

### I have become a **Scrum master**

* I know about the [scrum development process](https://www.atlassian.com/agile/scrum)

* I’ve read about [scrum development](https://www.atlassian.com/agile/tutorials/how-to-do-scrum-with-jira-software) with Jira

* I have read about scrum in data teams [here](https://towardsdatascience.com/agile-in-data-science-how-can-scrum-work-effectively-for-your-team-c567208e9d3f#:~:text=Scrum%20is%20an%20Agile%20framework,backlog%20and%20a%20sprint%20backlog.) and [here](https://www.datascience-pm.com/scrum/)

* I know about [CI/CD](https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment) and why data teams should also use it

### I have become a **Documentation advocate**

* I have documented learnings for reference

* I have written at least two blog posts on what I learned during my 90 days

* I have worked to improve my writing skills, including using [this](http://grammarly.com/), reading [this](https://towardsdatascience.com/the-importance-of-writing-as-a-data-scientist-22feb2b1d33d) and [this](https://www.grammarly.com/blog/how-to-improve-writing-skills/)
