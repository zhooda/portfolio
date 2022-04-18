---
title: "Enriched Funnels in SQL"
description: "A SQL exploration to help drill down into lower level metrics a basic funnel can't provide"
cover:
    caption: "A SQL exploration to help drill down into lower level metrics a basic funnel can't provide"
date: 2022-04-17T19:42:57-06:00
draft: false
author: Zeeshan Hooda
tags: ["SQL", "Big Data", "Analytics", "Event Driven Analytics", "Funnel"]
ShowToc: true
math: true
---

# Intro

Analytics funnels are generally used for measuring the conversion rates through a product. If we want to see the rates of users that visit your website, add something to their cart, and checkout, we'll use a generic analytics funnel which may look something like this:

![picture of funnel](/posts/funnel/funnel.png)
_Figure 1: Generic analytics funnel showing \_\_\_\_ conversion_

Many of us have heard of, and are intimately familiar with generic funnels, but what is an enriched funnel? An enriched funnel aggregation basically provides us with a funnel that has been enriched with some extra insights.

Let's take this example funnel, which shows a feature that lets customers in a retail store request help online and have an employee dispatched to them in-store:

| Step             | Count | Lag | Drop Off |
| ---------------- | ----: | --: | -------: |
| Product View     |   593 |     |          |
| Request Help     |   142 | 593 |     0.76 |
| Request Accepted |   127 | 142 |     0.11 |
| Help Arrived     |   101 | 127 |     0.20 |

Drop off is calculated as follows:

$$
\text{Drop Off} = 1 - \frac{lag(count, 1)~over~(~)}{count(*)}~~(1)
$$
