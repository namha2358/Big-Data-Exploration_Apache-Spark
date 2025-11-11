# Big-Data-Exploration_Apache-Spark
This project uses Apache Spark to explore a large public Crunchbase organizations dataset (~1.1M records) and practice distributed querying, text processing, and UDFs at scale.
Overview:
This project uses Apache Spark to explore a large public Crunchbase organizations dataset (~1.1M records) and practice distributed querying, text processing, and UDFs at scale. I built a small analytical playground in PySpark to perform pattern-based queries on company names, locations, and domains using the DataFrame API and custom functions.

Process:
Spark session & data ingestion:
Configured a local Spark environment (with findspark, Java, and SparkSession) and loaded the Crunchbase ODM Orgs CSV into a Spark DataFrame with schema inference and robust CSV parsing (multiLine, escape, PERMISSIVE mode). 
Inspected the schema and sampled rows to verify key columns such as name, city, region, country_code, domain, and social URLs.
Confirmed dataset scale with count(): 1,127,636 records. 

Name-based pattern queries:
Used Spark string functions split and size to find companies whose names contain exactly three words (e.g., "Fox Interactive Media"), counting ~206k such companies and previewing their locations. 
Created a Python UDF has_repeating_consecutive_letter to detect names with at least one pair of consecutive identical letters (e.g., “Facebook”, “Twitter”), applied it with filter, and found ~273k such companies. 


Location-based queries:
Filtered the dataset to all companies where region == "New Jersey", counted them (10,251), and selected just the name + location fields for inspection (city, region, country). 

Domain-based feature engineering:
Added a derived column TechDomain as a binary flag: 1 if the company’s domain contains "github.io", else 0.
Counted 81 such companies and listed their names and locations — a quick example of column-wise feature engineering using when / otherwise. 

Key Findings:
Even simple exploratory questions (e.g., “How many companies have three-word names?” or “How many are in New Jersey?”) become non-trivial at million-row scale, making Spark’s distributed DataFrame operations valuable. 

The custom UDF example demonstrates how to blend Python logic with Spark to perform complex text pattern detection across a very large dataset. 


Derived flags like TechDomain show how to quickly tag subsets of interest (e.g., developer-centric products hosted on GitHub Pages) for deeper analysis.
