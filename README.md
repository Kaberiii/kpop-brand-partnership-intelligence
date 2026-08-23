# K-pop Brand Partnership Intelligence Dashboard

### SQL Server | Power BI | Data Analysis

An end-to-end business intelligence project analyzing **121 K-pop celebrity-brand partnerships from 2016 to 2023**.

The project explores how brand partnerships are distributed across **artists, groups, entertainment companies, luxury and consumer brands, partnership types, and geographic markets**. The data was processed and modeled in **SQL Server**, followed by interactive visualization and analysis in **Power BI**.


## Project Overview

The growing relationship between K-pop and global brands has created a complex ecosystem of celebrity endorsements, ambassador roles, campaigns, and regional partnerships.

This project analyzes a dataset of K-pop celebrity-brand partnerships to answer questions such as:

* How has the number of recorded partnerships changed over time?
* Are brands more likely to partner with individual artists or groups?
* Which entertainment companies have the highest partnership volume?
* Which artists and brands appear most frequently in the dataset?
* How concentrated is the entertainment company landscape compared with the brand landscape?
* What types of partnerships are most common?
* What geographic markets do these partnerships target?
* Which entertainment companies have the most Global Ambassador partnerships?


# Dataset

The dataset contains **121 K-pop celebrity-brand partnership records** spanning **2016–2023**.

### Key fields include:

| Column         | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| Name_on_List   | Original artist/group identifier                                  |
| Name           | Individual idol name                                              |
| Gender         | Artist or group gender                                            |
| Solo_Group     | Indicates whether the partnership involves a solo artist or group |
| Group          | Associated K-pop group                                            |
| Company        | Entertainment company                                             |
| Parent_Brand   | Parent or primary brand                                           |
| Main_Brand     | Specific product or sub-brand                                     |
| Title          | Type of partnership or endorsement                                |
| Notes          | Additional partnership information                                |
| Date_announced | Date the partnership was announced                                |
| Region         | Geographic scope of the partnership                               |

The dataset was cleaned before being loaded into SQL Server.


# Tech Stack

* **SQL Server**
* **SQL Server Management Studio (SSMS)**
* **Power BI**
* **DAX**
* **Power Query**


# Project Architecture

```text
Raw Dataset
     │
     ▼
Data Cleaning
     │
     ▼
SQL Server Staging Layer
     │
     ▼
Dimension & Fact Tables
     │
     ▼
Analytical SQL Queries
     │
     ▼
SQL View
vw_kpop_brand_partnerships
     │
     ▼
Power BI
     │
     ▼
Interactive 3-Page Dashboard
```

# Data Modeling

The dataset was structured in SQL Server using a fact and dimension-based approach.

### Tables created

#### Fact Table

* `fact_partnership`

Stores partnership-level information such as:

* Artist/Idol
* Group
* Brand
* Entertainment company
* Partnership type
* Date announced
* Region

#### Dimension Tables

* `dim_idol`
* `dim_group`
* `dim_brand`

A consolidated analytical view was then created:

```sql
vw_kpop_brand_partnerships
```

This view was connected to Power BI for dashboard development.


# SQL Analysis

The SQL analysis included:

* Data cleaning and staging
* Fact and dimension table creation
* `JOIN`
* `GROUP BY`
* `COUNT()`
* `COUNT(DISTINCT ...)`
* `CASE`
* Common Table Expressions (CTEs)
* Window functions
* `LAG()`
* Year-over-year growth calculations
* Top-N analysis
* Percentage calculations
* Ranking and aggregation logic

# Key SQL Analysis Questions

The project explored several business questions.

### Market Overview

* How many partnerships are recorded in the dataset?
* How many unique artists, groups, brands, and entertainment companies are represented?
* How has partnership activity changed over time?
* What is the year-over-year growth rate?

### Talent Analysis

* Which individual artists have the highest number of partnerships?
* Are individual artists or groups more commonly involved in brand partnerships?
* Which entertainment companies represent the largest number of artists and partnerships?

### Brand Analysis

* Which brands have the highest number of partnerships?
* How concentrated is the brand partnership landscape?
* What proportion of partnerships is controlled by the top brands?

### Partnership Strategy

* Which partnership types are most common?
* How many Global Ambassador partnerships are represented?
* Which entertainment companies have the highest number of Global Ambassador deals?
* What is the geographic scope of partnerships?

# Power BI Dashboard

The final Power BI dashboard consists of **three analytical pages**.


## 01 — Market Overview

Provides a high-level view of the K-pop brand partnership landscape.

### Metrics and analysis include:

* Total Partnerships
* Unique Idols
* Unique Parent Brands
* Individual Partnership Percentage
* Partnership growth over time
* Individual vs Group partnerships
* Top brands by partnership count
* Distribution of partnership types

### Key question:

> What does the overall K-pop brand partnership market look like?


## 02 — Agency & Talent Intelligence

Focuses on the role of entertainment companies and individual artists.

### Metrics and analysis include:

* Top entertainment company
* SM partnership volume
* HYBE partnership volume
* SM + HYBE market share
* Partnership volume by entertainment company
* Top individual idols by partnership count
* Agency-level partnership distribution
* Individual vs group partnership mix by agency

### Key question:

> Which entertainment companies and individual artists dominate the partnership landscape?


## 03 — Brand & Partnership Strategy

Examines brand participation, partnership structures, and geographic reach.

### Metrics and analysis include:

* Unique Parent Brands
* Top 3 Brand Deals
* Top 3 Brand Share
* Global Ambassador Deals
* Top 10 brands by partnership count
* Distribution of partnership types
* Geographic scope of partnerships
* Global Ambassador partnerships by entertainment company

### Key question:

> How are brands structuring partnerships across relationship types and geographic markets?



# Key Insights

## 1. Sharp growth in recorded partnerships

The number of recorded partnerships increased from:

* **23 partnerships in 2022**
* **49 partnerships in 2023**

This represents a **113.04% year-over-year increase** in recorded partnerships within the dataset.

> This indicates a sharp increase in partnership activity represented in the available data, rather than necessarily proving that the entire K-pop endorsement industry doubled.


## 2. Individual artists dominate the dataset

Out of **121 partnerships**:

* **110 involved individual artists**
* **11 involved groups**

This means:

### **90.91% of recorded partnerships involved individual artists**

This suggests that, within this dataset, brands more frequently formed partnerships with individual K-pop personalities than with entire groups.


## 3. Entertainment company representation is concentrated

The two largest entertainment companies were:

| Entertainment Company | Partnerships |
| --------------------- | -----------: |
| SM                    |           30 |
| HYBE                  |           26 |

Together, SM and HYBE accounted for:

### **46.28% of all recorded partnerships**

This indicates a relatively concentrated entertainment company landscape within the dataset.


## 4. Brand participation is comparatively fragmented

The top three brands were:

* Dior
* Louis Vuitton
* Prada

Together, they accounted for:

* **18 partnerships**
* **14.88% of all partnerships**

This contrasts with the agency-side concentration.

### Key comparative insight:

> **Entertainment company representation is significantly more concentrated than brand participation in this dataset.**

While SM and HYBE account for **46.28%** of partnerships, the top three brands account for only **14.88%**.


## 5. Global Ambassador is the dominant partnership type

The dataset contains:

### **49 Global Ambassador partnerships**

This represents approximately:

### **40.50% of all recorded partnerships**

Global Ambassador roles form the largest partnership category in the dataset, followed by other structures such as Brand Ambassador, Muse, Campaign, and Endorsement Model.


# DAX Measures

Examples of measures used in Power BI include:

### Total Partnerships

```DAX
Total Partnerships =
COUNTROWS(vw_kpop_brand_partnerships)
```

### Unique Parent Brands

```DAX
Unique Parent Brands =
DISTINCTCOUNT(
    vw_kpop_brand_partnerships[parent_brand]
)
```

### Individual Partnership Percentage

```DAX
Individual Partnership % =
DIVIDE(
    CALCULATE(
        [Total Partnerships],
        vw_kpop_brand_partnerships[partnership_entity] = "Individual"
    ),
    [Total Partnerships]
)
```

### Top 3 Brand Deals

```DAX
Top 3 Brand Deals =
VAR TopBrands =
    TOPN(
        3,
        ALL(vw_kpop_brand_partnerships[parent_brand]),
        [Total Partnerships],
        DESC
    )
RETURN
    CALCULATE(
        [Total Partnerships],
        TopBrands
    )
```

### Top 3 Brand Share

```DAX
Top 3 Brand Share % =
DIVIDE(
    [Top 3 Brand Deals],
    [Total Partnerships]
)
```

### Global Ambassador Deals

```DAX
Global Ambassador Deals =
CALCULATE(
    [Total Partnerships],
    vw_kpop_brand_partnerships[title] = "Global Ambassador"
)
```


# Business Value

This project demonstrates how raw partnership data can be transformed into a structured business intelligence solution.

The analysis can help explore:

* Talent partnership concentration
* Entertainment company influence
* Brand portfolio activity
* Partnership positioning strategies
* Geographic reach
* Growth trends in recorded endorsement activity

The project also demonstrates an end-to-end analytics workflow, from **data preparation and relational modeling in SQL Server to interactive storytelling in Power BI**.


# Limitations

This analysis is based on the available dataset of **121 recorded partnerships** and should not be interpreted as a complete representation of the global K-pop endorsement industry.

Some records contain:

* Missing regional information
* Different naming conventions
* Variations in partnership titles
* Parent-brand and sub-brand distinctions

Therefore, the findings should be interpreted as insights from the **observed dataset**, rather than definitive estimates of the entire industry.

```md
![Market Overview](images/page1_market_overview.png)
```

Do the same for Pages 2 and 3. That will make the repository immediately understandable to a recruiter opening it for the first time.
