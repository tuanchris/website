---
title: Anatomy of a dbt project
image: https://cdn-images-1.medium.com/max/10000/0*1PfmQnADjrW73iep
description: Some basic concepts and project structure to help you get started with a dbt project.
---

For analysts not from a technical background, working with dbt can be intimidating at first. Writing codes to configure everything takes some time to get used to, especially if you are used to setting everything up using a UI.

If you consider dbt for your team or just started with a team that uses dbt, this post will hopefully help ease you into the project structure and some basic concepts. We will walk through most files and folders in the image below. You can file the repo [here](https://github.com/dbt-labs/dbt-init/tree/master/starter-project).

![Image from [dbt-init](https://github.com/dbt-labs/dbt-init/tree/master/starter-project) project.](https://cdn-images-1.medium.com/max/2480/1*bgUI3LTLdY19EFRwSyZh1A.png)*Image from [dbt-init](https://github.com/dbt-labs/dbt-init/tree/master/starter-project) project.*

## profiles.yml

This file contains the database connection that dbt will use to connect to the data warehouse. You only have to worry about this file if you set up dbt locally.

Since this file can have sensitive information such as project name and database credentials, it is not in your dbt project. By default, the file is created in the folder: ~/.dbt/.

If you start your project from scratch, running dbt init will generate this file for you. If not, you may have to create the .dbt folder and a profiles.yml file locally. Follow dbt [documentation](https://docs.getdbt.com/dbt-cli/configure-your-profile) or contact the repo owner if you are unsure how to set up this file.

If you work on multiple projects locally, the different project names (configured in the dbt_project.yml file) will allow you to set up various profiles for other projects.

Besides configuring the database connection, you can also configure a target. Target is how you have different configurations for different environments. For instance, when developing locally, you and your team would want separate datasets/databases to work on. But when deploying to production, it is best to have all tables in a single dataset/database. The default target is dev.

## dbt_project.yml

This file is the main configuration file for your project. If you are creating your project, change the project name and the profile name (preferably to the same value). Also, replace my_new_project at the models section with the new project name.

All objects in this project will inherit settings configured here unless overridden at the model level. For example, you can configure to create all models as tables in the dbt_project.yml file. But you can go into one of the models and override that setting to create a view instead.

Where to configure what depend on your project setup, but a good principle to follow is DRY (do not repeat yourself). For settings that apply to the whole project or a specific folder, define here in this file. For options that are only relevant to one model, configure it there.

For a complete list of settings, you can configure in this file, check out the dbt_project.yml [documentation](https://docs.getdbt.com/reference/dbt_project.yml).

## models

The models folder contains all data models in your project. Inside this folder, you can create any folder structure that you want. A recommended structure put out in the dbt [style guide](https://github.com/dbt-labs/corp/blob/master/dbt_style_guide.md) is as follow:

    ├── dbt_project.yml
    └── models
        ├── marts
        |   └── core
        |       ├── intermediate
        |       |   ├── intermediate.yml
        |       |   ├── customers__unioned.sql
        |       |   ├── customers__grouped.sql
        |       └── core.yml
        |       └── core.docs
        |       └── dim_customers.sql
        |       └── fct_orders.sql
        └── staging
            └── stripe
                ├── base
                |   ├── base__stripe_invoices.sql
                ├── src_stripe.yml
                ├── src_stripe.docs
                ├── stg_stripe.yml
                ├── stg_stripe__customers.sql
                └── stg_stripe__invoices.sql

Here, we have the marts and staging folders underneath models. Different data sources will have separate folders underneath staging (e.g. stripe). Use cases or departments have different folders underneath marts (e.g. core or marketing).

Notice the .yml and .doc files in the example above. They are where you would define metadata and documentation for your models. You can have everything in the dbt_project.yml file, but it is much more cleaner to define them here.

This structure allows you to organize objects clearly and easily apply bulk settings.

## data

This folder contains all manual data that will be loaded to the database by dbt. To load the .csv files in this folder to the database, you will have to run the dbt seed command.

Since this is a version-controlled repository, do not put large files or files with sensitive information here. A file that is changed regularly is also not a good candidate for this approach. Some examples of a good fit for dbt seed are yearly budget, status mappings, category mappings, etc.

## macros

Macros in dbt are similar to functions in excel. You can define custom functions in the macros folder or override default macros and macros from a package. [Macros, together with Jinja templating](https://docs.getdbt.com/docs/building-a-dbt-project/jinja-macros), gives you many functionalities that are not available with SQL.

For example, you can use a control structure (if statements and for loops) or different behavior for different targets. You can also abstract away complicated SQL logic and makes your code much more readable.

    -- This is hard to read
    (amount / 100)::numeric(16, 2) as amount_usd

    -- This is much easier
    {{ cents_to_dollars('amount') }} as amount_usd

## packages.yml

One of the great things about dbt is that you can easily use packages that others have made. Doing so can save you tons of time, and you will not have to reinvent the wheel. You can find most of the dbt packages [here](https://hub.getdbt.com/).

To use any of these packages, you need to define them in the packages.yml file. Simply add content as following to the file.

    packages:
      - package: dbt-labs/dbt_utils
        version: 0.7.3

Before you can use these packages, you have to run dbt deps to install these dependencies. After that, you can use any macro from the packages in your cod.

## snapshot

Snapshot is a dbt feature to capture the state of a table at a particular time. The snapshot folder contains all snapshots models for your project, which must be separate from the model folder.

The use case for this is to build a slowly changing dimension (SCD) table for sources that do not support change data capture (CDC). For example, every time the status of an order change, your system overrides it with the new information. In this case, there we cannot know what historical statues that order had.

Snapshot offers a solution around this. If you capture the orders tables every day, you can keep the history of order status changes over time. For every record, dbt will determine whether it is the latest one and update the old one’s effective period.

![Image from dbt [documentation](https://docs.getdbt.com/docs/building-a-dbt-project/snapshots)](https://cdn-images-1.medium.com/max/2000/1*UenQCtO0h2WLAWW5lK67DQ.png)*Image from dbt [documentation](https://docs.getdbt.com/docs/building-a-dbt-project/snapshots)*

Read more about the dbt snapshot function [here](https://docs.getdbt.com/docs/building-a-dbt-project/snapshots).

## tests

Most of the tests in a dbt project are defined in a .yml file under models. These are tests that use pre-made or custom macros. These tests can be applied to a model or a column.

![Image from dbt [documentation](https://docs.getdbt.com/docs/building-a-dbt-project/tests)](https://cdn-images-1.medium.com/max/2000/1*65vBHGQB1CXpJMrtRwsY3A.png)*Image from dbt [documentation](https://docs.getdbt.com/docs/building-a-dbt-project/tests)*

In the example above, when you run dbt test, dbt will check whether orer_id is unique and not_null, status are in the defined values, and every records of customer_id can be linked to a record in the customers table.

Sometimes though, these tests are not enough, and you need to write custom ones. In that case, you would store those custom tests in the tests folder. dbt will evaluate the SQL statement. The test will pass if no row is returned and failed if at least one or more rows are returned.

## Conclusion

We have walked through some basic concepts and project structure of a typical dbt project in this post. I hope that this can be the start of a fascinating new journey for you.

Happy learning✌️
