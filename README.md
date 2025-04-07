# Dimensional-Modelling-Invoice-Based

A complete guide to building a scalable and analytical star schema data warehouse using invoice transaction data. This project applies dimensional modeling principles to transform raw invoice data into a well-structured, high-performance model optimized for business intelligence (BI) and reporting use cases.

## Project Description

In today’s data-driven economy, organizations must make quick and accurate decisions based on transactional data. This project presents a dimensional model built from invoice data using a **Star Schema** design. It incorporates best practices for data profiling, fact/dimension table design, handling slowly changing dimensions (SCDs), and implementing an efficient ETL pipeline.

**Project Scope**: Design, model, and document a dimensional data warehouse  
**Focus Areas**: Data profiling, modeling (Star Schema), ETL strategy, performance tuning  
**Target Outcome**: Enable efficient BI reporting and sales analytics across products, customers, time, and stores.

## Key Objectives

- Profile invoice data to identify relevant dimensions and facts.
- Design a Star Schema data warehouse with clear business logic.
- Implement support for Slowly Changing Dimensions (SCD Types 1 & 2).
- Build an ETL pipeline (Extract, Transform, Load) that maintains data quality and performance.
- Address data modeling assumptions and trade-offs with justifications.

## Dimensional Model Design

### Star Schema Structure

- **Fact Table**: `Fact_Invoice`
- **Dimension Tables**:
  - `Dim_Customer`
  - `Dim_Product`
  - `Dim_Date`
  - `Dim_Store`

Each dimension connects to the central fact table through foreign keys. This design simplifies querying and improves performance.

### Fact_Invoice Table

| Column         | Type     | Description                                 
|----------------|----------|---------------------------------------------
| Invoice_ID     | String (PK) | Unique invoice transaction ID              
| Date_ID        | Integer (FK) | Reference to `Dim_Date`               
| Customer_ID    | String (FK) | Reference to `Dim_Customer`            
| Product_ID     | String (FK) | Reference to `Dim_Product`             
| Store_ID       | String (FK) | Reference to `Dim_Store`                
| Quantity       | Integer     | Units purchased                         
| Unit_Price     | Decimal     | Cost per unit                          
| Line_Total     | Decimal     | Quantity × Unit_Price                

## Dimension Tables Overview

### `Dim_Customer`
| Column           | Description                          |
|------------------|--------------------------------------|
| Customer_ID (PK) | Unique identifier                    |
| Customer_Name    | Full name                            |
| Customer_Segment | Regular, VIP, etc.                   |
| Location         | Region or city                       |

### `Dim_Product`
| Column        | Description                           |
|---------------|---------------------------------------|
| Product_ID (PK)| Unique identifier                    |
| Product_Name  | Product name                          |
| Category      | Electronics, Accessories, etc.        |
| Price         | Unit price                            |

###  `Dim_Date`
| Column         | Description                         |
|----------------|-------------------------------------|
| Date_ID (PK)   | Surrogate key                       |
| Date           | Actual date                         |
| Day, Month, Year, Quarter, Day_of_Week | Time breakdown |

### `Dim_Store`
| Column         | Description                        |
|----------------|------------------------------------|
| Store_ID (PK)  | Unique store identifier            |
| Store_Location | City or region                     |
| Store_Type     | Online, Physical                   |


## ETL Process Overview

### Extract
- Sources: POS systems, CSV, MySQL/PostgreSQL
- Tools: Python (Pandas), SQL, Talend, Apache NiFi

### Transform
- Clean, deduplicate, enrich (e.g., Line_Total = Quantity × Unit_Price)
- Handle SCDs and validate referential integrity

### Load
- Load dimension tables first, followed by the fact table
- Target warehouse: Snowflake, Redshift, BigQuery
- Tools: Apache Airflow, AWS Glue

## Data Modeling Best Practices

### Data Quality Strategies
- Standardized formats
- Null value checks
- Referential integrity enforcement
- Duplicate removal

### Handling Slowly Changing Dimensions (SCDs)
- **SCD Type 1**: Minor corrections (e.g., name typos)
- **SCD Type 2**: Track changes in customer segments and product categories

## Business Value Delivered

- **Sales Trend Analysis**: Time-series sales reporting across products and stores
- **Customer Insights**: Segmentation, loyalty, and purchasing patterns
- **Product Performance**: Identify bestsellers by location and time
- **Store Performance**: Benchmark store-level revenue and transactions

## Assumptions & Trade-Offs

### Assumptions
- Invoice data is immutable
- No nulls in key columns
- Batch ETL preferred over real-time
- SCD Type 2 applied where history is relevant


### Design Trade-Offs
| Decision                    | Justification                       |
|-----------------------------|-------------------------------------|
| Star Schema vs Snowflake    | Chose Star for simplicity/speed     |
| SCD Type 2 vs Type 1        | Chose Type 2 for historical tracking|
| Batch vs Real-Time ETL      | Chose Batch for maintainability     |
| Invoice-level Date Granularity | Adequate for reporting needs     |

---

## Final Conclusion

This dimensional model is optimized for performance, analytics, and long-term scalability. It enables a business to gain meaningful insights into customer behavior, sales trends, and store performance, while offering clean ETL processes and support for historical reporting.

## Project Files

- `Invoice_Dimensional_Model_Report.pdf`: Full modeling documentation
- `Star_Schema_Diagram.png`: Data model architecture (attach if available)
- `ETL_Pipeline_Flow.pdf`: Visual breakdown of ETL process (optional)




---
