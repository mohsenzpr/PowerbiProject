Online Retail Sales – Power BI Dashboard

This project is an end-to-end BI case study built on the **UK Online Retail** dataset from Kaggle.  
I created it as a portfolio project to showcase how I think about **data cleaning, modeling, and dashboard design** in Power BI.

---

1. Data Preparation – Key Decisions

- **Optimized data types**  
  Converted text columns to numeric where possible to reduce model size and improve performance.

- **Separated invoice status from invoice number**  
  One column mixed letters and numbers (e.g., `C12345`) where the letter meant *cancelled invoice*.  
  I:
  - extracted the letter into a separate **True/False “IsReturn” flag**  
  - converted the remaining part into a **numeric invoice ID**  
  This keeps business meaning while making the column usable in the model.

- **Handled missing Customer IDs without losing data**  
  Many rows had no Customer ID.  
  - I **kept these rows** so sales, product, and country totals stay accurate.  
  - For **customer-level analysis (RFM, segmentation)** I excluded them, so the segmentation is not biased by “anonymous” customers.

---

2. Data Modeling & DAX – Key Decisions

- **Used a star-schema model**  
  Built one main fact table (sales) and separate dimensions for **Date, Customer, Product, Time, Location** to keep relationships simple and scalable.

- **Implemented dynamic RFM in DAX**  
  Instead of calculating RFM once in Power Query, I calculated **Recency, Frequency, Monetary and RFM scores in DAX**, so segmentation updates automatically with filters (date, country, etc.).

- **Separated segmentation logic from raw data**  
  Created a small **Customer Segmentation table** (e.g., Champions, Loyal, At Risk, Lost…) and mapped RFM scores to labels.  
  This makes slicers cleaner and the logic easier to maintain.

- **Centralized KPIs in a measure table**  
  All important metrics (Total Sales, AOV, Return Rate, etc.) live in a single measure table, which keeps the model organized and easier to extend.

---

3. Dashboard Design – Key Decisions

The report has **three pages**, each with a specific question in mind:

- **Sales Dashboard (Landing)** – “What is happening in the business?”  
  - High-level KPIs (Sales, Invoices, AOV, Customers, Return Rate)  
  - Monthly sales, top products, sales by country, return rate by month  
  - Global filters (Month, Day, Hour) and navigation buttons

- **Customer Analysis** – “Who are our customers?”  
  - RFM-based segmentation donut chart  
  - Top returning customers  
  - Customer count by month  
  Focus: understanding customer value and engagement.

- **Location Analysis** – “Where and when do we sell?”  
  - AOV by country  
  - Hour × Day sales heatmap to spot peak times  
  - Interactive map with a tooltip showing per-country KPIs and RFM mix  

Design choices focused on **simple navigation, minimal color palette, and business-readable labels** rather than technical terms.
