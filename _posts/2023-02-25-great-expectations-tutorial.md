---
layout: post
title:  "Great expectations data pipeline tool tutorial"
date:   2023-02-25 00:00:00 +0000
categories: data pipelines great-expectations tool
---
[Great expectations](https://greatexpectations.io/){:target="_blank"} is a nice tool for building data pipelines.

There are two versions of it:
1. GX Open Source
2. GX Cloud

GX Open Source is the open source community based offering while GX Cloud is the managed cloud hosted offering. We will evaluate the GX open source version today.

As the [page](https://greatexpectations.io/gx-oss){:target="_blank"} says
`
A powerful, flexible data quality solution
Profile, test, and document with an open source platform developed by data engineers, for data engineers.
`

To get started, please follow [this link](https://docs.greatexpectations.io/docs/tutorials/getting_started/tutorial_overview/){:target="_blank"}.

Install GX Open Source:

pre-requisites:
- python (3.7 - 3.10)
- git
- pip

Get the data:
`git clone https://github.com/great-expectations/gx_tutorials
cd gx_tutorials`

`pip install great_expectations`

`great_expectations --version`

O/p
`great_expectations, version 0.15.50`

Create a data context:

Data context -> manages project configuration

Initialize your great expectations deployment for the project:
`great_expectations init`

Great expectations will create a new directory with the following structure:

    great_expectations
    |-- great_expectations.yml
    |-- expectations
    |-- checkpoints
    |-- plugins
    |-- .gitignore
    |-- uncommitted
        |-- config_variables.yml
        |-- data_docs
        |-- validations

OK to proceed? [Y/n]: <press Enter>

Press enter to continue. You will have your directory structure and configuration files. All these are your data context.

O/p
Congratulations! You are now ready to customize your Great Expectations configuration.

You can customize your configuration in many ways. Here are some examples:

  Use the CLI to:
    - Run `great_expectations datasource new` to connect to your data.
    - Run `great_expectations checkpoint new <checkpoint_name>` to bundle data with Expectation Suite(s) in a Checkpoint for later re-validation.
    - Run `great_expectations suite --help` to create, edit, list, profile Expectation Suites.
    - Run `great_expectations docs --help` to build and manage Data Docs sites.

  Edit your configuration in great_expectations.yml to:
    - Move Stores to the cloud
    - Add Slack notifications, PagerDuty alerts, etc.
    - Customize your Data Docs

Please see our documentation for more configuration options!

we are done with the first step. I will share very soon the second step related to connecting to data. Stay tuned!