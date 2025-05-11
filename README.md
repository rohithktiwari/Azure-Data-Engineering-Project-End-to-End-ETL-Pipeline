# Building an End-to-End Data Engineering Solution with Azure ✨

In this blog, I share a comprehensive guide to designing an end-to-end (E2E) data engineering pipeline using Azure's powerful tools. The project processes, transforms, and delivers data for Business Intelligence (BI) purposes, leveraging resources like Azure Data Factory, Azure Databricks, Azure Synapse Analytics, and Power BI. The data source is the **AdventureWorks dataset**, fetched directly from GitHub. Here’s how the solution is structured:


![project](https://github.com/user-attachments/assets/7c51260a-236e-43ae-a965-91508684014c)


---
## 📌 Project Objective

To build a scalable, secure, and efficient data pipeline that:
- Ingests data from external sources
- Transforms and cleans the data using PySpark
- Stores data in a structured format for analysis
- Enables rich visualizations for decision-making

---

## 🧱 Architecture Overview

```plaintext
         [External API Source]
                  |
          Azure Data Factory (ADF)
                  |
        Azure Data Lake Storage Gen2
        ┌──────────┬──────────┬──────────┐
     [Bronze Layer][Silver Layer][Gold Layer]
                  |
          Azure Databricks (PySpark)
                  |
        Azure Synapse Analytics (SQL Pools)
                  |
             Power BI Dashboard
```

---

## **Architecture Overview**

### **Step 1: Setting Up the Azure Environment** ⚙️

To start, the following Azure resources were provisioned:

- **Azure Data Factory (ADF):** Used for data orchestration and automation.
- **Azure Storage Account:** Acts as the data lake, storing raw (bronze), transformed (silver), and curated (gold) data.
- **Azure Databricks:** Performs data transformations and computations.
- **Azure Synapse Analytics:** Handles data warehousing for BI use.

All resources were configured with proper Identity and Access Management (IAM) roles to ensure seamless integration and security.
  ![Screenshot 2025-05-11 093649](https://github.com/user-attachments/assets/6000d4ce-73ad-4aa0-91bf-72bdd34ccce0)



---

### **Step 2: Implementing the Data Pipeline Using ADF** 🚀

**Azure Data Factory (ADF)** serves as the backbone for orchestrating the data pipeline.

1. **Dynamic Copy Activity:**
   - ADF pulls data from GitHub using an HTTP connector and stores it in the bronze container in Azure Storage.
   - Parameters were added to the pipeline for adaptability to changes in the data source.
  
     ![Screenshot 2025-05-11 095951](https://github.com/user-attachments/assets/6fa006fd-c18a-4a04-aa56-c7e2af168fb9)



The raw data is now securely stored and ready for transformation.

![Screenshot 2025-05-11 100041](https://github.com/user-attachments/assets/ce9849a9-b053-4a1c-bff2-0ab0c893802e)



---

### **Step 3: Data Transformation with Azure Databricks** 🔄

Using Azure Databricks, the raw data from the bronze container was transformed into a structured format.

#### Key Steps:
- **Cluster Setup:** A Databricks cluster was created to process the data efficiently.
- **Data Lake Integration:** Databricks connected to Azure Storage to access the raw data.

 ![Screenshot 2025-05-11 100136](https://github.com/user-attachments/assets/4f7bb41c-4942-4095-9fbc-4c93c12a49fb)



#### Transformations:
- Normalized date formats for consistency.
- Cleaned and filtered invalid or incomplete records.
- Grouped and concatenated data to make it more usable for analysis.
- Saved the transformed data in the silver container in Parquet format for optimal storage and query performance.

  ![Screenshot 2025-05-11 101737](https://github.com/user-attachments/assets/b249ef96-5774-470a-be5c-439f0d1c5789)


![Screenshot 2025-05-11 102641](https://github.com/user-attachments/assets/b37885a9-9e66-4e42-9786-b24d233f13b3)

  



---

### **Step 4: Data Warehousing with Azure Synapse Analytics** 📊

Azure Synapse Analytics structured the processed data for analysis and BI reporting.

#### Steps:
1. **Connection to Silver Container:** Configured Synapse to query data directly from Azure Storage.
2. **Serverless SQL Pools:** Enabled querying without provisioning upfront resources.
3. **Database and Schema Creation:**
   - Created SQL databases and schemas to organize data.
   - Defined external tables and views for BI consumption.
  
     ![Screenshot 2025-05-11 102005](https://github.com/user-attachments/assets/72d41fcd-cf64-4979-b908-810a15bd759f)

  ![Screenshot 2025-05-11 102101](https://github.com/user-attachments/assets/d0d9e234-252d-4ac4-ac4b-d67c0672720e)

   



The cleaned, structured data was then moved to the gold container for reporting purposes.

![Screenshot 2025-05-11 102158](https://github.com/user-attachments/assets/adb76f5c-5397-4192-adfe-77e317f23bc3)



---

### **Step 5: Business Intelligence Integration** 🕵️‍♂️

The final step involved integrating the data with a BI tool to visualize and generate insights.

- **Power BI Integration:**
   - Connected Power BI to Azure Synapse Analytics.
   - Designed dashboards and reports to present actionable insights to stakeholders.
 
     ![Screenshot 2025-05-11 102952](https://github.com/user-attachments/assets/87125fd7-e9ca-4556-ad8b-ce0cceeb7462)


---

## 🗂️ Project Breakdown

### 1️⃣ Data Ingestion (Bronze Layer)
- Extracted data from an external HTTP API using Azure Data Factory.
- Stored raw data in Azure Data Lake Storage Gen2 in a structured folder format.

### 2️⃣ Data Transformation (Silver Layer)
- Created a secure connection between Azure Data Lake and Databricks using Microsoft Entra ID (App ID, Secret, Tenant ID).
- Used PySpark to clean, filter, and transform the raw data.
- Implemented **incremental loading** using SCD Type 1 (Upsert logic) for optimized performance.

### 3️⃣ Data Serving (Gold Layer)
- Loaded transformed data into **Azure Synapse Analytics** using `OPENROWSET()` and **external tables**.
- Enabled fast, structured access for analytical querying.

### 4️⃣ Reporting and Dashboard
- Connected **Power BI** to Synapse Analytics.
- Built a real-time, interactive dashboard to visualize the final business insights.

---

## 💡 Key Learnings

- Understanding the Medallion Architecture in real-world data workflows.
- Connecting Azure services securely using managed identities and service principals.
- Handling incremental data loads for scalable ETL.
- Query optimization in Synapse using external tables and views.
- Delivering insights through Power BI dashboards.

---

This end-to-end solution exemplifies how modern data-driven businesses can leverage Azure to transform raw data into meaningful insights, driving informed decision-making. ✅

---

## **Acknowledgment** 🎉

This project draws inspiration from an insightful [GitHub repository by Ansh Lamba](https://github.com/anshlambagit). For a detailed video walkthrough, check out his [YouTube channel](https://www.youtube.com/watch?v=0GTZ-12hYtU&t=15907s&ab_channel=AnshLamba). Special thanks to Ansh for providing such valuable resources and guidance for aspiring data engineers!


## 📬 Contact

If you have any questions, ideas, or want to collaborate — feel free to connect!

**Author:** Rohit Tiwari
**LinkedIn:** [linkedin.com/in/rohithktiwari](https://www.linkedin.com/in/rohithktiwari/)  
**Email:** rohithktiwari@gmail.com
