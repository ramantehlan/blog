---
title: "Part-1: Introduction to Data Mining"
date: 2020-03-03T21:43:19+05:30
lastmod: 2020-03-03T21:43:19+05:30
draft: true
keywords: []
description: ""
tags: []
categories: []
author: "Raman Tehlan"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: true
postMetaInFooter: true
hiddenFromHomePage: true
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

<!--more-->

Data is growing at astonishing rates, it is being created every second. [In 2020, every person will generate 1.7 megabytes every second](https://www.domo.com/learn/data-never-sleeps-6). This data is powerful, it helps in making data-informed decisions. For example, [Netflix saves $1 billion per year on customer retention](https://insidebigdata.com/2018/01/20/netflix-uses-big-data-drive-success/), they use data to create its strategy to lower subscription cancellation rates by adjusting or adding new features.

Data generated is most often in a very raw format and it's very hard to make sense of it. Which is why we need to process it to get more sophisticated information out of it. **Data Mining is the process of extracting information from a large amount of data**. Given data of ample size and quality, data mining provides the following capabilities:

- **Predictive**: Predict trends and behaviours.
- **Desciptive**: Discover unknown patterns.

# Tasks

The data mining process involves 6 common classes of tasks:

1. Anomaly Detection
2. Association Rule Learning
3. Clustering
4. Classification
5. Regression
6. Summarization

## 1. Anomaly Detection
<center>
<img src="https://user-images.githubusercontent.com/29037312/75864107-8bc68480-5e27-11ea-855c-14a17e132145.png" alt="Anomaly Detection" width="350">

*[Source: Engineering.com](https://www.engineering.com/AdvancedManufacturing/ArticleID/19058/Anomaly-Detection-Industrial-Asset-Insights-Without-Historical-Data.aspx)*
</center>

The **process to recognize unusual data records, that might be an outlier/change/deviation/noise/error** that requires further examination. This process is also used in a variety of domains, such as intrusion detection, fraud detection, fault detection, system health monitoring, event detection in sensor networks and detecting ecosystem disturbances.

## 2. Association Rule Learning
<center>
<img src="https://user-images.githubusercontent.com/29037312/75864127-92ed9280-5e27-11ea-9805-540ca59f4641.png" alt="association rule learning" width="350">

*[source: wikipedia](https://en.wikipedia.org/wiki/association_rule_learning)*
</center>

it is used to **discover relationships between data variables to create a dependency model**. The most popular example is [affinity analysis or market basket analysis](https://www.wikiwand.com/en/Affinity_analysis), let's say from the store data we can determine which product or combination of products are frequently bought together, we can use this information for promotional pricing, product placements or marketing. It is also used for web usage mining, continuous production and bioinformatics.

## 3. Clustering
<center>
<img src="https://user-images.githubusercontent.com/29037312/75864147-97b24680-5e27-11ea-8336-c0fff0e52b90.png" alt="clustering" width="350">

*[Source: datanovi](https://www.datanovia.com/en/lessons/clara-in-r-clustering-large-applications/)*
</center>

The **task of grouping data which is in some way or another "similar"**, without using known structures in the data. It is many fields, including machine learning, pattern recognition, image analysis, information retrieval, bioinformatics, data compression, and computer graphics.

## 4. Classification
<center>
<img src="https://user-images.githubusercontent.com/29037312/75864157-9b45cd80-5e27-11ea-8140-6bbb15662a41.png" alt="clustering" width="350">

</center>

The **task of mapping new or existing data into a set of categories, based on the features of data**. Applications of classification are in domains like computer vision, drug discovery and development, geostatistics, speech recognition, statistical NLP, pattern recognition, recommender system etc.

## 5. Regression
<center>
<img src="https://user-images.githubusercontent.com/29037312/75864168-9da82780-5e27-11ea-8b17-b3e7673048fe.png" alt="clustering" width="350">
</center>

It is a **task to find a function which models the data with least error**. It is to estimate the relationships between dependent variables (outcome variables) and one or more independent variables(predictors or features). It is used for sales/market forecasts, risk analysis for investments, quality control, human resources.

## 6. Summarization
<center>
<img src="https://user-images.githubusercontent.com/29037312/75879218-03ed7400-5e41-11ea-8f6e-7b838ee163e5.png" alt="clustering" width="600">

*Different visualizations used in summarization. Source:[Morphocode](https://morphocode.com/location-time-urban-data-visualization/)*
</center>

It is a **task of providing a more compact representation of the data set**, including visualization and report generation.

# Architecture
<center>
<img src="https://user-images.githubusercontent.com/29037312/75909603-69a62400-5e72-11ea-84a8-7a23020ed874.png" alt="clustering" width="400">

*This is the standard data mining architecture. Source: [ResearchGate](https://www.researchgate.net/figure/The-architecture-of-a-data-mining-system_fig1_323401290)* </center>



