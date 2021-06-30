---
template: post
title: What is Data Engineering?
slug: what-is-de
socialImage: https://www.7wdata.be/wp-content/uploads/2019/07/data-engineer-jobjpg.png
draft: true
date: 2021-06-30T02:19:26.608Z
description: An introduction to Data Engineering
category: Data Engineering
tags:
  - DE
---
## What is Data Engineering?

To make data driven decisions in life or in business, we need to have good quality data to make the right analysis. The process of making this good quality data available is what we call Data Engineering. A good analogy here would be a need to build a flyover road within a city. We would need Civil Engineers for planning, designing, and overseeing construction and maintenance. We need Data Engineers to design, implement and maintain Data pipelines. We can visualize it as a superset of Business Intelligence, Data Warehousing and Software Engineering.

Who are Data Engineers?

A Data Engineer is a Software Engineer with specialized skills. They build interfaces and mechanisms to enable flow and access of information (Data) from a producer to a consumer. Being well versed with key design principles of Data Architecture and Data Pipeline design is a must to be successful as a Data Engineer.

Why is this field important?

Data Engineering is an underrated field, partly because of a lack of ways to show for it. In contrast, the work of a Data Analyst by the nature of the work is most seen via dashboards/visualizations. Data Infrastructure and good quality data are of utmost importance. Without a strong foundation, no amount of fancy dashboards can be helpful.

Let’s look at Tesla’s Autopilot - FSD as an example. A Model S or any other Tesla car with FSD enabled is (almost) able to drive without human intervention. How does Tesla achieve this? Well Tesla cars pack many sensors. The data from these sensors feeds into some kind of deep neural net model. The model handles making predictions on how to handle the car.

How is the deep neural net model trained? Tesla uses live data from all the different Tesla cars that are being driven all across the world. Now how does this live data get fed into the process of training the model? A data pipeline designed to ingest this real time sensor data achieves this feat. At a high level, the data pipeline has three components. First, a process to ingest this sensor data. Second, a process to clean, apply validations and transform the ingested data. Finally the data pipeline loads the processed data into a Data Warehouse.

What’s a Data Warehouse?

A Data Warehouse is a database which contains processed information. The Data undergoes a process called normalization.To save storage space and make analytical queries fast we use. Two of the most popular ones - Star and Snowflake schemas.

How is Data Ingested into a Data Warehouse?

A process called ETL (Extract, Transform, Load) is used to ingest data from a raw data source into the Data Warehouse. The “Transform” process is used to clean, confirm and process the data to fit into the rigid schemas that we talked about before.