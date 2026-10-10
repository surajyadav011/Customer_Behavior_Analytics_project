# Real Customer Behavior Analysis

A complete **end-to-end analytics pipeline** that takes raw customer data all the way through cleaning, database design, querying, and interactive visualization. This is what a professional data analyst does.

---

## **The End-to-End Story**

This isn't just "I made a chart." This is a complete analytics workflow:

```
Messy CSV File
     ↓
Python (Clean & Transform)
     ↓
PostgreSQL Database (Real Data Storage)
     ↓
10 SQL Queries (Answer Business Questions)
     ↓
Power BI Dashboard (Interactive Insights)
     ↓
Stakeholders Make Decisions
```

**What makes this "end-to-end":**
- You don't just analyze the data, you own the entire pipeline
- Every step depends on and validates the previous one
- The dashboard updates live from the database
- Non-technical users can explore without asking you for custom reports
- The entire process is reproducible with different data

This is professional analytics. This is what hiring managers look for.

---

## **What This Project Does**

We analyzed 3,900 customer records across different categories, looking at spending patterns, subscription behavior, discount effectiveness, and product performance. The goal was simple: understand what drives customer purchases and where revenue really comes from. But we did it the right way—through a complete, professional pipeline.

---

## **Project Flow**

```
Raw CSV Data
     ↓
Python (Jupyter) - Clean & Transform
     ↓
PostgreSQL - Ask the Real Questions
     ↓
Power BI - Tell the Story with Visuals
```

This is the analyst workflow. Each step builds on the last, and you can't skip any of them.

---

## **Folder Structure**

```
customer-behavior-analysis/
│
├── data/
│   └── customer_shopping_behavior.csv     (Original dataset - 3,900 records)
│
├── notebooks/
│   └── real_customer_behavior_project.ipynb
│       ├── Data Loading & Exploration
│       ├── Data Cleaning (null values, column formatting)
│       ├── Feature Engineering (age groups, purchase frequency)
│       ├── PostgreSQL Connection Setup
│       └── Data Export to Database
│
├── sql/
│   └── customer_behavior_sql_query.sql
│       ├── Q1: Revenue by Gender
│       ├── Q2: Discount Analysis
│       ├── Q3: Top 5 Products by Rating
│       ├── Q4: Shipping Type Comparison
│       ├── Q5: Subscription Impact
│       ├── Q6: Discount Penetration by Product
│       ├── Q7: Customer Segmentation (New/Returning/Loyal)
│       ├── Q8: Top 3 Products per Category
│       ├── Q9: Repeat Buyers & Subscription Correlation
│       └── Q10: Revenue by Age Group
│
├── dashboards/
│   └── Customer_Behavior_analysis.pbix    (Power BI Desktop file)
│       ├── KPI Cards (Customers, Avg Purchase, Review Rating)
│       ├── Subscription Distribution
│       ├── Revenue by Category & Age Group
│       ├── Sales by Category & Age Group
│       └── Interactive Filters
│
└── README.md                              (This file)
```

---

## **Why This Is An End-to-End Pipeline**

Most people can make a chart. That's not analytics. That's just visualization.

Real analytics owns the entire pipeline:

**Messy CSV → Clean Data → Database → Business Queries → Interactive Dashboard → Decisions**

### **What You Own:**

✅ **Data Quality** - You clean it, you know it works  
✅ **Database Design** - You build it, you know the structure  
✅ **Query Logic** - You write it, you know what it measures  
✅ **Visualization** - You design it, stakeholders explore on their own  
✅ **Reproducibility** - Same process, different data, different business  

### **What This Means:**

- This isn't a one-off analysis that sits in a folder
- This is a system you can run again next month, next quarter, next year
- This is a system you can hand to someone else and they can use it
- This is a system that grows with the business

**Most analysts are journalists - they report what they find.**  
**Good analysts are engineers - they build systems that find answers.**

This project shows you how to be an engineer.

---

## **Part 1: Jupyter Notebook - Getting Your Data Ready**

Think of this as data janitorial work. You get messy data, and you make it clean enough to ask real questions.

### **What We Did:**

1. **Loaded the CSV** - Started with 3,900 customer records
2. **Checked for Problems** - Looked at missing values, data types, duplicates
3. **Filled Missing Data** - Review ratings had gaps, so we filled them with the median rating per category (median is safer than average for this)
4. **Cleaned Column Names** - Changed "Purchase Amount (USD)" to simple "purchased_amount"
5. **Created New Columns** - Built age groups (Young Adult, Adult, Middle-aged, Senior) from raw age numbers
6. **Mapped Values** - Turned "Fortnightly" into actual numbers (14 days) for easier analysis later

### **Why This Matters:**

You could skip to the fancy Power BI dashboard, but you'd miss this: most analytics work is actually data cleaning. Real data is messy. People type things differently, systems have bugs, sensors fail. Cleaning is where analysts earn their paycheck.

Here's what the raw data looks like (first few rows):

![Jupyter Notebook - Data Cleaning and Loading](https://raw.githubusercontent.com/your-username/customer-behavior-analysis/main/screenshots/01_jupyter_notebook.png)

The notebook handled everything from column renaming to creating meaningful age segments. By the end, we had a clean table ready for PostgreSQL.

---

## **Part 2: PostgreSQL - Asking the Right Questions**

Raw clean data is great, but data that answers business questions is better.

### **The 10 Questions We Asked:**

| Question | What It Tells Us |
|----------|-----------------|
| Q1: Revenue by Gender | Who spends more - men or women? |
| Q2: High Spenders with Discounts | Do discounts attract people who would buy anyway? |
| Q3: Top 5 Products by Rating | What products do customers love? |
| Q4: Shipping Type Impact | Does faster shipping increase purchase amounts? |
| Q5: Subscription Power | Do subscribers actually spend more? |
| Q6: Discount Penetration | Which products get the deepest discounts? |
| Q7: Customer Segments | How many new, returning, and loyal customers do we have? |
| Q8: Category Winners | What are the top 3 bestsellers in each category? |
| Q9: Repeat Buyer Behavior | Do frequent buyers subscribe more? |
| Q10: Age Group Revenue | Which age group brings in the most money? |

### **Example Query - Subscription Impact:**

```sql
select subscription_status,
count(customer_id) as total_customers,
round(avg(purchased_amount),2) as avg_spend,
round(sum(purchased_amount),2) as total_revenue
from customer
group by subscription_status
order by total_revenue,avg_spend desc;
```

This one query shows us three things at once: how many subscribers we have, what they spend on average, and their total contribution to revenue. That's efficient querying.

Here's the actual database setup (PostgreSQL with pgAdmin):

![PostgreSQL Database - Customer Table Schema](https://raw.githubusercontent.com/your-username/customer-behavior-analysis/main/screenshots/02_postgresql_setup.png)

All 10 queries are in the `sql/` folder. Each one is written to be readable. Good SQL is commented SQL.

---

## **Part 3: Power BI Dashboard - Telling the Story**

Charts and dashboards exist for one reason: to make numbers make sense in seconds instead of minutes.

### **What's on the Dashboard:**

**Top Row - The Headline Numbers**
- 3.9K Total Customers
- $59.76 Average Purchase Amount  
- 3.75 Average Review Rating

**Left Side - Distribution & Patterns**
- Subscription Status Split (27% yes, 73% no)
- Revenue by Category (Clothing leading at 164K)
- Sales by Age Group (Young Adults dominating)

**Right Side - Filters You Can Play With**
- Subscription Status (Yes/No)
- Gender (Male/Female)
- Category (Clothing, Accessories, Footwear, Outerwear)
- Shipping Type (6 different options)

### **Why These Visualizations?**

Each chart answers a specific question:
- **Pie Chart** for "What % of our customers subscribe?" - percentages are what pie charts do best
- **Bar Chart** for "Which category makes the most revenue?" - comparing values across categories
- **KPI Cards** for "What's our baseline?" - quick reference numbers

Here's the actual dashboard in action:

![Power BI Dashboard - Customer Behavior Insights](https://raw.githubusercontent.com/your-username/customer-behavior-analysis/main/screenshots/03_powerbi_dashboard.png)

The dashboard is interactive. Click a filter and everything updates. This is what stakeholders love because they can explore without asking you for custom reports.

---

## **Key Findings**

These numbers came directly from the SQL queries and ended up in the Power BI dashboard:

### **Revenue Insights**
- Clothing category generates 164K (highest)
- Young Adults are the biggest spenders (52K revenue)
- Subscription customers spend more on average but not dramatically more

### **Customer Behavior**
- 73% of customers don't subscribe - opportunity here
- 27% of customers subscribe and we should keep them happy
- 15% of customers get discounts but spend more than average anyway (good sign)

### **Product Performance**
- Every category has clear winners (top 3 products carry most sales)
- Products with high ratings also get purchased frequently
- Discount rate varies by product - some need discounts more than others

---

## **Technical Stack**

| Tool | Purpose | Why |
|------|---------|-----|
| **Python (Pandas)** | Data cleaning & transformation | Fast, flexible, industry standard |
| **PostgreSQL** | Relational database & SQL queries | Reliable, scales well, great for business logic |
| **Power BI** | Interactive dashboards & visualization | Business users get it, self-service exploration |
| **Jupyter Notebook** | Code documentation & reproducibility | Run once, explain everything, keep forever |

---

## **How to Use This Project**

### **If You Want to Learn From It:**

1. Start with the Jupyter notebook - see how real data gets cleaned
2. Read through the SQL file - see how questions become queries
3. Open the Power BI file - see how queries become insights
4. Follow the exact flow - Jupyter → SQL → BI is the real workflow

### **If You Want to Adapt It:**

1. Replace the CSV file with your own customer data
2. Update column names in the notebook if needed
3. Modify the SQL queries to match your business questions
4. Recreate the Power BI visualizations with your data
5. Adjust the dashboard filters based on what matters to your business

### **Database Setup (PostgreSQL):**

```
Username: postgres
Password: suraj1234
Host: localhost
Port: 5432
Database: real customer behaviour
Table: customer
Records: 3,900
```

Make sure PostgreSQL is running before you run the notebook's data export step.

---

## **What You'll Learn**

This project teaches you the complete analytics pipeline:

1. **Data thinking** - How to explore unfamiliar data without breaking it
2. **SQL skills** - How to write queries that answer real questions
3. **Visualization thinking** - Which chart type tells which story
4. **Communication** - How to take your analysis and show it to humans
5. **Workflow** - The actual sequence analysts follow in the real world

It's not just about the code. It's about the approach.

---

## **Questions to Ask Your Own Data**

If you're adapting this, ask yourself:

- Who are your power users? (Like our "high spenders with discounts")
- What percentage subscribe/stay active/come back?
- How does one segment behave differently from another?
- Where is revenue concentrated? (We found it in Young Adults + Clothing)
- Which of your top products are actually profitable?

Good analysis starts with good questions.

---

## **Files Explained**

- **real_customer_behavior_project.ipynb** - The whole analysis from start to finish. Run it and watch the flow.
- **customer_behavior_sql_query.sql** - Copy-paste these into your database tool. They're production-ready.
- **Customer_Behavior_analysis.pbix** - Open in Power BI Desktop. Explore the dashboard. Click the filters.
- **customer_shopping_behavior.csv** - The original dataset. 3,900 rows of customers and their purchases.

---

## **Next Steps**

This project is a foundation. You can extend it:

- Add time series analysis (how do purchases trend week to week?)
- Build a customer lifetime value model
- Predict who's likely to churn
- Segment customers for targeted marketing
- Track dashboard metrics monthly for trends

The infrastructure is here. The questions are endless.

---

## **Author**

Built by someone learning data analytics the right way - from raw data to real insights.

If you found this useful, that's the whole point. Good analysis should be reproducible and learnable.

---

---

## **The End-to-End Professional Perspective**

If you walk into a data job interview and they ask "Tell us about your analytics project," here's what you should say about this one:

"I took raw customer data and built an end-to-end pipeline. I cleaned the data in Python, loaded it into a PostgreSQL database, wrote 10 business-specific SQL queries, and built an interactive Power BI dashboard. The system is reproducible - we can update it with new data and everything refreshes automatically. Stakeholders can explore the data themselves through filters instead of asking me for custom reports. This is the workflow I use for any customer dataset."

That's a job-ready answer.

This project shows:
- Technical depth (Python, SQL, database design, visualization)
- Business thinking (asking the right questions, understanding the customer)
- Professional maturity (building systems, not just reports)
- Reproducibility (same process, any data)
- Communication (dashboards non-technical people understand)

This is what companies hire data analysts to do.

---

**Last Updated:** October 2026

**Data Period:** Customer transaction records analyzed

**Tools:** Python, PostgreSQL, Power BI, SQL

**Project Type:** End-to-End Analytics Pipeline

**Workflow Maturity:** Production-Ready

---

*This is a real project that went through a real workflow. The data is realistic but anonymized. The analysis is genuine. The insights are actionable. The pipeline is reproducible. The process is scalable.*

*This is professional analytics.*
