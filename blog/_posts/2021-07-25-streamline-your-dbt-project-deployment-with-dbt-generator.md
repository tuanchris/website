---
title: Streamline your dbt project deployment with dbt-generator
image: https://cdn-images-1.medium.com/max/12000/0*RSt_oBbPydgMnkgP
description: Running 50 commands to generate base models? Writing the same transforms for the 100 times for your base models? This package will streamline this process for you.
---

# Streamline your dbt project deployment with dbt-generator

We love dbt, and we use it for almost all of our consulting projects. There are so many cool pre-made packages in the [dbt hub](https://hub.getdbt.com/) that dramatically improves your productivity. For example, Fivetran has created pre-made starter models for many common sources such as Hubspot, Salesforce, Google Ads, and Facebook Ads. Fishtown Analytics also created some great starters packages, such as dbt-utils, audit-helper, and code-gen.

When starting a project with a new client, we often go through the same steps to set up a new dbt project. After integrating data from sources to a data warehouse, we use the code-gen package to generate source schemas with all the tables in it. We also use the same package to generate base models for our tables, where we can rename columns and do some simple transformations.

For smaller clients or sources with fewer tables, this is totally fine. However, when you have ten plus tables in a source, running the same amount of commands to generate base models can start to feel daunting. Additionally, the same source often has the same naming conventions for its columns. Our time can be better spent elsewhere than changing write_at columns to modified_date for the 50 times.

## dbt-generator

Introducing [dbt-generator](https://pypi.org/project/dbt-generator/) 🎉🎉. I wrote a simple Python package to help with this problem.

This package helps in generating the base models and transform them in bulk. For sources with 10+ models, this package will save you a lot of time by generating base models in bulk and transform them for common fields. Using this package is a great way to start your modeling or onboarding new sources.

## Getting started

To use this package, you need dbt installed with a profile configured. You will also need to install the code-gen package from dbt Hub. Add the following to the packages.yml file in your dbt repo and run dbt deps to install dependencies.

    packages:
      - package: fishtown-analytics/codegen
        version: 0.3.2

Install the package in the same environment with your dbt installation by running:

    pip install dbt-generator

This package should be executed inside your dbt repo. Source code for this package can be found here:
[**GitHub - tuanchris/dbt-generator: Generate and process base models for dbt**
*This package helps in generating the base models and transform them in bulk. For sources with 10+ models, this package…*github.com](https://github.com/tuanchris/dbt-generator)

## Generate base models

To generate base models, use the dbt-generator generate command. This is a wrapper around the codegen command that will generate the base models. This is especially useful when you have a lot of models, and you want to generate them all at once.

    Usage: dbt-generator generate [OPTIONS]

      Gennerate base models based on a .yml source

    Options:
      -s, --source-yml PATH   Source .yml file to be used
      -o, --output-path PATH  Path to write generated models
      --source-index INTEGER  Index of the source to generate base models for
      --help                  Show this message and exit.

### Example

    dbt-generator generate -s ./models/source.yml -o ./models/staging/source_name/

This will read in the source.yml file and generate the base models in the staging/source_name folder. If you have multiple sources defined in your yml file, use the --source-index flag to specify which source you want to generate base models for.

## Transform base models

For the same source, you often have consistent naming conventions between tables. For example, the created_at and modified_at fields are often named the same for all tables. Changing all these fields to common values across different sources is a best practice. However, doing that for all the date columns in 10+ tables is a pain.

With this package, you can write a transforms.yml file that will be read in (the .yml file can be named anything). This file will contain the transforms that you want to apply to all the base models. You can just rename the fields in the base models or apply a custom SQL select to the transformed fields.

    Usage: dbt-generator transform [OPTIONS]

      Transform base models in a directory using a transforms.yml file

    Options:
      -m, --model-path PATH       The path to models
      -t, --transforms-path PATH  Path to a .yml file containing transformations
      -o, --output-path PATH      Path to write transformed models to
      --drop-metadata BOOLEAN     The drop metadata flag
      --case-sensitive BOOLEAN    The case sensitive flag
      --help                      Show this message and exit.

### Example

    ID:
      name: ID
      sql: CAST(ID as INT64)
    CREATED_TIME:
      name: CREATED_AT
    UPDATED_TIME:
      name: MODIFIED_AT
    DATE_START:
      name: START_AT
    DATE_STOP:
      name: STOP_AT

This .yml file when applied to all models in the staging/source_name folder will cast all ID field to INT64 and rename all the date columns to a value in the name key. For example, CREATED_TIME will be renamed to CREATED_AT and DATE_START will be renamed to START_AT. If no sql is provided, the package will just rename the field. If a sql is provided, the package will execute the SQL and rename the field using the name key.

    dbt-generator transform -m ./models/staging/source_name/ -t ./transforms.yml

This will transform all models in the staging/source_name folder using the transforms.yml file. You can also drop the metadata by setting the drop-metadata flag to true (dropping columns start with _). The --case-sensitive flag will determine if the transforms will use case-sensitive names or not.

## Limitations

Here are some of the limitations of the current release. If you want to contribute, please open an issue or a pull request.

* Transforms only works with model generated with the code-gen package.

* You cannot transform a model that has already been transformed

* You cannot use wild card in fields selection for transforms (e.g. *_id)

* No tests yet

* No error handling yet
