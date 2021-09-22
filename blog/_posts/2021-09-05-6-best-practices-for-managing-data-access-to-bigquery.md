---
title: 6 Best Practices for Managing Data Access to BigQuery
image: https://cdn-images-1.medium.com/max/5514/0*PP7AJcQwfTIfFebh
description: What to know in terms of security when setting up a data environment in BigQuery.
---

We have all seen and heard about data breaches and the damages, both in terms of financial and reputation, that they can inflict. As we rely more and more on our data to make better decisions, data is becoming a critical asset for any organization. So like any other asset of a company, controlling access to data is essential to protecting your data.

Fortunately, modern data warehouses have great functionalities built-in to control precisely who has access to what. This is often referred to as Identity and access management or IAM. Cloud providers often design multiple layers to control access to data, and this post aims to shed some light on how Google does it with BigQuery.

However, it can be challenging to know the best practices in controlling access with the many control layers. This post attempts to lay out some recommended practices that I have come across over the years.

## How resources are organized in Google Cloud

BigQuery is Google’s technology of choice for data warehousing. To understand how to control access to BigQuery, you first have to understand how resources are organized in Google Cloud.

![Image from Google Cloud’s [documentation](https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-tw)](https://cdn-images-1.medium.com/max/2000/0*E6R2SWvEWvV6r-66)*Image from Google Cloud’s [documentation](https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-tw)*

The way Google Cloud is structured, we can grant access either at the **resource level** or any **hierarchical level**, such as project, folder, and organization.

You can grant permissive IAM at a hierarchical level if you don’t need fine-grained access at the resource level. In other words, if all people are allowed to access every dataset and table inside a project, there is no need to define permission at the resource level explicitly.

However, if you are still reading this article, you most likely want to control who can access what inside a project.

## Access Control Pattern For BigQuery

### Grant Fine-grained access at the resource level

![Photo by [Lutz Wernitz](https://unsplash.com/@luwe83?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/12032/0*gqU7truTlM-gofyK)*Photo by [Lutz Wernitz](https://unsplash.com/@luwe83?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

To query a table in BigQuery, you need two permissions: permission to** run the query** and **view the data**.

The permission to run queries can be defined at any of the hierarchical levels. You can be strategic about setting query run permission to have better visibility. For example, if the data processing is separated into different projects, you can view all the queries cost, query log, and data access log related to data transformations and consumption separately.

The permission to view data can also be set at a hierarchical level. However, it is highly recommended that you set this permission at the project or resource level (dataset and table). The rule of thumb is that if a role should have access to all data in a project, grant it at the project level. If you need to limit access to a certain dataset or table, grant the permission at the resource level.

BigQuery also has the ability to set up row-level and column-level security to allow for even more fine-grained access control. This will make a good topic for another post.

### Least privilege

![Photo by [FLY:D](https://unsplash.com/@flyd2069?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/13900/0*L3V0OTD3bjZuGqX8)*Photo by [FLY:D](https://unsplash.com/@flyd2069?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

In layman’s terms, Least Privilege means giving the least amount of permission required to perform a duty. The principle helps create a separation of duties for entities (users, groups & service accounts) and GCP resources. Least Privilege is the recommended practice for security on many systems.

For example, a data analyst’s duty is to query and aggregate transformed data. For this role, she should be given read-only access to transformed data to perform her job. Giving write access can mean that the data integrity can be at risk. The data analyst in this example can mistakenly delete or alter the production data. Similarly, an operation data analyst only needs access to operational data and not full financial or customer data.

Giving full access to a project (owner or editor permission) to everyone is often a mistake. By default, Google Cloud creates a compute service account with Editor permission to enable the compute API in a project. This account is very permissive and can be a potential security threat. It is best practice to disable the auto-creation of this account or remove it afterward.

### User service accounts for services.

![Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/12336/0*qCZUyRhi00BuBrDo)*Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

There are two main kinds of authentication that you can use in Google Cloud: **User Account** and **Service Account**. User Account is the Google Account that you use to log in to the console. On the other hand, Service Account is a JSON key file that you can use to authenticate services.

The difference between the two authentication methods is who is making the action. For the User Account, the user logs in with his username/password and performs the actions. For Service Account, it is a service (an ETL job, a visualization tool, a metadata catalog tool) performing the action.

A common mistake here is to use one User Account to authenticate for services. Doing this will run into quota problems and make it harder to control access and audit logs.

Another common mistake is to use one Service Account for every service. This is also not a recommended practice since you will not know what service makes what actions. Moreover, since the account is used for all services, it will be permissive and increase the chance of a breach.

### Grant access to groups instead of individual accounts

![Photo by [Margarida CSilva](https://unsplash.com/@marg_cs?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/8544/0*m5UllFY6THLvf44w)*Photo by [Margarida CSilva](https://unsplash.com/@marg_cs?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

The main reason for doing this is to have better control over IAM permissions in a project. Imagine if you have ten people that need access to data in a project + five different service accounts, maintaining who has access to what can quickly get out of hands.

However, the number of roles will be significantly lower (or, at worst, equal) than the number of people. Therefore, a better approach is to create a different group based on roles and add permission accordingly for more clarity.

You can also add a group as a member of another group for an extra layer of control. For example, you can have a data analyst group. Inside that group, you can have a marketing analyst group, an operational analyst group, etc.

### Use infrastructure-as-code (IaC)

![Photo by [Daniele Colucci](https://unsplash.com/@daniele71043?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/12000/0*we_mCHgThJW2j9J_)*Photo by [Daniele Colucci](https://unsplash.com/@daniele71043?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

IaC enables you to create different environments easily, especially when your project is complex and has many moving parts. On a large project, you can have environments with complex permissions and policies. Writing code for one environment once and provision the same thing for the staging and development environment can save you time.

With IaC, every change in your environment is versioned, so you know who makes what changes (given that you limit admin permissions to only your IaC service). You can also periodically scan your environments for differences between the configurations and the actual environments. Most IaC services will then revert your environment to the configurations if they detect any alternations.

Check out some of my other articles on this topic below.
[**Data lake on GCP using Terraform**
*Use Terraform to set up infrastructure-as-code for a Data Lake on Google Cloud Platform.*towardsdatascience.com](https://towardsdatascience.com/data-lake-on-gcp-using-terraform-469062a205ad)
[**Bootstrap a Modern Data Stack in 5 minutes with Terraform**
*Setup Airbyte, BigQuery, dbt, Metabase, and everything else you need to run a Modern Data Stack using Terraform.*towardsdatascience.com](https://towardsdatascience.com/bootstrap-a-modern-data-stack-in-5-minutes-with-terraform-32342ee10e79)

### Separation of resources

![Photo by [Guillaume Bolduc](https://unsplash.com/@guibolduc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/8860/0*0fBNOC6XmSOVRNGe)*Photo by [Guillaume Bolduc](https://unsplash.com/@guibolduc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

One of the best ways to enforce security is to have separations of resources. That means creating different projects altogether for data that you don’t want to be stored together.

A good place to start is to separate resources between ingestion, processing, and access to ensure that data is only accessed on a needed basis. With this design, you can lock down raw data ingestion and control what data is available at the access layer. A common use case is to mask or hash personal identifiable information (PII) before exposing the tables to the data warehouse.

## Conclusion

In a modern cloud platform, such as Google Cloud, there are many layers to limit data access. I discussed using the following best practices to make sure that you have a secured data environment:

* Grant Fine-grained access at the resource level

* Least privilege

* User service accounts for services.

* Grant access to groups instead of individual accounts

* Use infrastructure-as-code (IaC)

* Separation of resources

In a later post, I will share how to use row-level security, column-level security, and VPC service control to have an even more secured data environment.

Cheers ✌️
