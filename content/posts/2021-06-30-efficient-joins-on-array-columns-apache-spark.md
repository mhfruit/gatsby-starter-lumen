---
template: post
title: Efficient joins on array columns - Apache Spark
slug: apache-spark-array-contains
socialImage: https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Apache_Spark_logo.svg/1200px-Apache_Spark_logo.svg.png
draft: true
date: 2021-06-30T02:15:17.109Z
description: A curious case of joins
category: Data Engineering
tags:
  - Spark
---
## A Peculiar Situation

A few weeks back at work, I came across a peculiar problem which goes something like this. Within one of the workloads, I had to join two tables in Spark with one table having the join column of the type Array.

The tables were moderate in size, while trying to process the workload I noticed Spark was preparing to run around 200000 tasks and the whole workload took close to 2 hours to complete. This situation was puzzling to me. Why would Spark want to create so many tasks for moderately sized workloads.

I opened up Spark UI and right there I could see a stage displaying a logical plan involving a Cartesian Product while resolving the join within the stage. Okay, Why would there be a Cartesian Product within the logical plan? Maybe something to do with my join condition containing array_contains.

Investigating further (multiple google searches) got me to a JIRA link on Apache Spark. So apparently, if you choose to use array_contains within the join, a cartesian product will appear in your logical plan against the join, this is due to the way array_contains transformation is implemented at the Optimizer level.

Thanks to Nikolas Vanderhoof, if you manually apply the optimization as follows. A join like this:

```scala
left.join(
  right,
  array_contains(left("arr"), right("value")) // Cartesian product in logical plan
)
```

will produce the same results as:

```scala
{
  val leftPrime = left.withColumn("exploded_arr", explode(col("arr")))

  leftPrime.join(
    right,
    leftPrime("exploded_arr") === right("value") // Fast equijoin
  ).drop("exploded_arr").distinct
}

```

Spark would use an equijoin and my workload execution time reduced from 2 hours to 5 mins.