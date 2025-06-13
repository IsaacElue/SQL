# Layoffs Data Analysis Project

This repository contains a SQL project focused on cleaning and exploring a dataset of company layoffs. The project aims to identify trends, patterns, and interesting insights within the global layoffs data.

# Introduction
This project is an end-to-end data analysis pipeline, starting from raw data, duplicated, moving through a rigorous cleaning process, and concluding with exploratory data analysis (EDA) to uncover meaningful patterns. The primary goal was to practice basics and solidify SQL data cleaning and analysis techniques using a real-world dataset.

# Background
The dataset used in this project is sourced from Kaggle: Layoffs 2022. It contains information about company layoffs, including company name, location, industry, total laid off, percentage laid off, date, funding stage, country, and funds raised in millions. This data provides a rich ground for understanding the impact of economic shifts and other factors on global employment.

This project was completed as a follow-along guide to learn and implement practical SQL skills.

# Tools I Used
MySQL Workbench: Used for database management, running SQL queries, and visualizing the data.

SQL (Structured Query Language): The core language used for all data manipulation, cleaning, and analysis tasks.

Kaggle Dataset: The source of the raw layoffs data.

# The Analysis
The analysis was divided into two main phases: Data Cleaning and Exploratory Data Analysis (EDA).

Data Cleaning (DATA CLEANING PROJECT.sql)
This phase involved several crucial steps to ensure data quality and consistency:

Duplicate Removal:

Initially, I identified duplicates based on key columns (company, industry, total_laid_off, date).

To handle complex duplicates accurately, a staging table (layoffs_staging2) was created with an added row_num column using ROW_NUMBER() over a partition of all relevant columns. This allowed for precise identification and deletion of truly redundant entries.

Data Standardization and Error Fixing:

Industry: Handled NULL and empty string values by setting them to NULL and then updating them where possible by joining on company name to propagate existing industry values.

Industry Variations: Standardized variations like 'Crypto Currency' and 'CryptoCurrency' to simply 'Crypto'.

Country: Cleaned up inconsistent country names, specifically removing trailing periods (e.g., "United States." became "United States").

Date Format: Converted the date column from a text format (%m/%d/%Y) to a proper DATE data type using STR_TO_DATE and ALTER TABLE.

Null Value Handling:

Reviewed NULL values in total_laid_off, percentage_laid_off, and funds_raised_millions. It was decided to keep these as NULL as they are useful for calculations during EDA.

Column and Row Removal:

Identified and removed rows where both total_laid_off and percentage_laid_off were NULL, as these provided no useful information for analysis.

Removed the temporary row_num column added during the duplicate removal phase.

Exploratory Data Analysis (EDA) (DATA EXPLORATION PROJECT.sql)
After cleaning, the data was explored to discover insights:

Overall Layoff Metrics:

Calculated the maximum number of total_laid_off in a single event.

Examined the percentage_laid_off to understand the scale of layoffs, identifying companies with 100% layoffs (often startups).

Analyzed companies with 100% layoffs, ordered by funds_raised_millions, revealing insights into failed ventures like Quibi.

Aggregated Layoffs:

Identified companies with the highest total layoffs.

Aggregated layoffs by location, country, year, industry, and stage to find key affected areas and sectors.

Advanced Analysis:

Company Layoffs Per Year: Used Common Table Expressions (CTEs) and DENSE_RANK() to rank companies by total layoffs per year, showing the top 3 companies with the most layoffs each year.

Rolling Total of Layoffs: Calculated a rolling sum of total layoffs per month, providing a cumulative view of the layoff trends over time. This involved extracting the year and month from the date column using SUBSTRING.

# What I Learned
Throughout this project, I gained valuable experience in:

Database Setup: Creating and populating staging tables for safe data manipulation.

Advanced SQL Techniques: Proficiently using ROW_NUMBER(), PARTITION BY, STR_TO_DATE(), TRIM(), UPDATE with JOIN, and CTEs for complex queries.

Data Quality: The importance of thoroughly checking for and addressing duplicates, inconsistencies, and null values.

Data Standardization: Best practices for unifying data entries (e.g., industry names, country names, date formats).

Exploratory Data Analysis: How to systematically query and aggregate data to uncover meaningful trends and outliers.

Problem-Solving: Approaching data challenges methodically, such as updating null values based on other records for the same entity.

#  Conclusions
This project successfully demonstrated a comprehensive data cleaning and exploratory analysis workflow using SQL. Key insights gained include:

The significant impact of layoffs across various industries and locations, particularly noting the vulnerability of startups.

Trends in layoffs over different years and the cumulative effect observed through rolling totals.

The effectiveness of SQL in preparing raw data for insightful analysis.

This project provided a solid foundation in practical SQL skills and data analysis methodologies, which are crucial for any data-driven role.