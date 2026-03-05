# Google Store Revenue Analysis: From BigQuery to R
An end-to-end data pipeline: SQL extraction from BigQuery (GA4 public dataset) followed by deep-dive analysis in R. This project identifies key revenue drivers by browser segmentation, utilizing tidyverse for data wrangling and ggplot2 for high-impact visualization.

Step-by-step workflow

# 1. Data Extraction (SQL & BigQuery)
Instead of using a static CSV, I performed a targeted feature selection directly from the bigquery-public-data.google_analytics_sample.

Action: Written a SQL query to unnest hits and extract key dimensions: deviceCategory, browser, country, and transactions.
Logic: Handled data scaling by converting transactionRevenue from micro-units to USD (Revenue/1,000,000).

# 2. Data Cleaning & Wrangling (R - Tidyverse)
Raw marketing data is notoriously "noisy." I used the Tidyverse ecosystem to sanitize the dataset.

Cleaning: Applied janitor::clean_names() for consistent snake_case naming.
Missing Values: Addressed the high sparsity of the dataset (90% NA in revenue) by using replace_na() to represent non-converting sessions as $0$.
Feature Engineering: Created a logical is_buyer flag to segment converting vs. non-converting users for more precise grouping.

# 3. Exploratory Data Analysis (EDA)
I conducted a deep dive into revenue distribution across different browsers to identify technical "Gold Mines."

Metric: Aggregated total revenue and transaction counts.
Refinement: Filtered out low-traffic browsers to avoid statistical noise in the visualization.

# 4. Data Visualization (ggplot2)

Design: Developed a horizontal bar chart using coord_flip() and theme_minimal() for executive-level readability.
Ranking: Used reorder() to rank browsers by financial impact rather than alphabetical order, making the "Chrome dominance" immediately apparent to stakeholders.

[ 👉 Click here to visualize the report](http://www.francescaetnom.com/Google_Merchandise_Analysis/google_store_analysis.html)
# 💡Key Business Insights
Browser Monoculture: Chrome accounts for the overwhelming majority of total revenue, suggesting the store's UX is highly optimized for the Google ecosystem.
ROI Strategy: Future development and A/B testing should prioritize Chrome and Safari, as other browsers show marginal financial contribution despite existing traffic.

# 📂Project Structure
google_store_analysis.Rmd: The source code including narrative and analysis.
google_store_analysis.html: The final knitted report.
google_analytics_data.csv: Sample of the extracted BigQuery dataset.
