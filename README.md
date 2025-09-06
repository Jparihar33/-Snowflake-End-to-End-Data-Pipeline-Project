Snowflake End-to-End Data Pipeline Project

##  Project Overview

This project implements a complete **end-to-end data pipeline** in **Snowflake**, using a **multi-zone architecture**:

- **Landing Zone**: Raw ingestion layer
- **Curated Zone**: Cleaned, enriched, and transformed data
- **Consumption Zone**: Final dimensional models used for reporting and analytics

The pipeline processes and integrates three core datasets:
- **Customer**
- **Item**
- **Orders**

---

##  Data Zone Architecture

### 1. **Landing Zone** (`MY_DB.LANDING_ZONE`)
- **Purpose**: Stores raw CSV or JSON data loaded from external sources.
- **Tables**: 
  - `LANDING_CUSTOMER`
  - `LANDING_ITEM`
  - `LANDING_ORDER`
- **Key Features**:
  - No transformations applied
  - Schema matches raw input files
  - Often contains strings for all fields (to handle bad/missing values)

---

### 2. 🧹 **Curated Zone** (`MY_DB.CURATED_ZONE`)
- **Purpose**: Applies data cleansing, validation, and type conversion.
- **Tables**:
  - `CURATED_CUSTOMER`
  - `CURATED_ITEM`
  - `CURATED_ORDER`
- **Key Transformations**:
  - Null/blank handling
  - Type casting (e.g., price from string to float)
  - Date parsing and formatting
  - Deduplication
  - Filtering out invalid records

---

### 3. 📊 **Consumption Zone** (`MY_DB.CONSUMPTION_ZONE`)
- **Purpose**: Contains final dimensional models and facts used for analytics or reporting.
- **Tables**:
  - `CUSTOMER_DIM`
  - `ITEM_DIM`
  - `ORDERS_FACT`
- **Key Features**:
  - Slowly Changing Dimension (SCD) logic
  - Aggregated facts for reporting
  - Optimized schema for BI tools (star schema)
