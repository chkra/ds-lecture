---
title: "Workshop: 06 Klassisches Data Engineering"
layout: single
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
author_profile: true
author: Christina Kratsch
lecture_name: "Data Science"
lecture_desc: "Grundlegende Methoden für die Exploration und das Management von Daten."
licence: "CC-BY"
licence_desc: 2024 | HTW Berlin 
classes: wide
---

### 🚀 Challenge #1: At the airport

You have been provided a [database](https://raw.githubusercontent.com/Microsoft/Data-Science-For-Beginners/main/2-Working-With-Data/05-relational-databases/airports.db) built on [SQLite](https://sqlite.org/index.html) which contains information about airports. The schema is displayed below. You will use the [SQLite extension](https://marketplace.visualstudio.com/items?itemName=alexcvzz.vscode-sqlite&WT.mc_id=academic-77958-bethanycheum) in [Visual Studio Code](https://code.visualstudio.com?WT.mc_id=academic-77958-bethanycheum) to display information about different cities' airports.

#### Instructions

To get started with the assignment, you'll need to perform a couple of steps. You'll need to install a bit of tooling and download the sample database.

#### Setup your system

You can use Visual Studio Code and the SQLite extension to interact with the database.

1. Navigate to [code.visualstudio.com](https://code.visualstudio.com?WT.mc_id=academic-77958-bethanycheum) and follow the instructions to install Visual Studio Code
1. Install the [SQLite extension](https://marketplace.visualstudio.com/items?itemName=alexcvzz.vscode-sqlite&WT.mc_id=academic-77958-bethanycheum) extension as instructed on the Marketplace page

#### Download and open the database

Next you will download an open the database.

1. Download the [database file from GitHub](https://raw.githubusercontent.com/Microsoft/Data-Science-For-Beginners/main/2-Working-With-Data/05-relational-databases/airports.db) and save it to a directory
1. Open Visual Studio Code
1. Open the database in the SQLite extension by selecting **Ctl-Shift-P** (or **Cmd-Shift-P** on a Mac) and typing `SQLite: Open database`
1. Select **Choose database from file** and open the **airports.db** file you downloaded previously
1. After opening the database (you won't see an update on the screen), create a new query window by selecting **Ctl-Shift-P** (or **Cmd-Shift-P** on a Mac) and typing `SQLite: New query`

Once open, the new query window can be used to run SQL statements against the database. You can use the command **Ctl-Shift-Q** (or **Cmd-Shift-Q** on a Mac) to run queries against the database.

For more information about the SQLite extension, you can consult the [sqlite documentation](https://marketplace.visualstudio.com/items?itemName=alexcvzz.vscode-sqlite&WT.mc_id=academic-77958-bethanycheum).

#### Database schema

A database's schema is its table design and structure. The **airports** database as two tables, `cities`, which contains a list of cities in the United Kingdom and Ireland, and `airports`, which contains the list of all airports. Because some cities may have multiple airports, two tables were created to store the information. In this exercise you will use joins to display information for different cities.

| Cities           |
| ---------------- |
| id (PK, integer) |
| city (text)      |
| country (text)   |

| Airports                         |
| -------------------------------- |
| id (PK, integer)                 |
| name (text)                      |
| code (text)                      |
| city_id (FK to id in **Cities**) |

#### Assignment

Create queries to return the following information:

1. all city names in the `Cities` table
1. all cities in Ireland in the `Cities` table
1. all airport names with their city and country
1. all airports in London, United Kingdom

### 🚀 Challenge #2: Coca Cola

#### Instructions

The Kaggle Account of user Yiyi Wang hosts a [Coca Cola data set](https://www.kaggle.com/yiyiwang0826/cocacola-excel), stored in a large Excel table. This Coca Cola Co spreadsheet is missing some calculations. 
Visit the account and, if necessary, inform yourself on the relevance of [Kaggle](https://www.kaggle.com/) - a site every data scientist should know. 

Study the data set description on Kaggle. After that, your task is to: 

1. Calculate the Gross profits of FY '15, '16, '17, and '18
    - Gross Profit = Net Operating revenues - Cost of goods sold
1. Calculate the average of all the gross profits. Try to do this with a function.
    - Average = Sum of gross profits divided by the number of fiscal years (10)
    - Documentation on the [AVERAGE function](https://support.microsoft.com/en-us/office/average-function-047bac88-d466-426c-a32b-8f33eb960cf6)
1. This is an Excel file, but it should be editable in any spreadsheet platform


### 🚀 Challenge #3: Principal Component Analysis

Principal Component Analysis is a very well established method to visualize high-dimensional data sets. Inform yourself on the mathematical bassis of the method using Wikipedia, ChatGPT, [SciKit Learn](https://scikit-learn.org/stable/modules/decomposition.html) or other sources. 

After that, 
1. study the [scikit learn demo for PCA](https://scikit-learn.org/stable/auto_examples/decomposition/plot_pca_iris.html#sphx-glr-auto-examples-decomposition-plot-pca-iris-py) on a very famous data set
2. try to apply PCA methods on a data set of your choice.
  
