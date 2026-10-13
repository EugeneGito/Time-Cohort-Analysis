# Customer Cohort Analysis: Do New Customers Come Back, and What Are They Worth?

A cohort analysis of UK online retail customers, built in Python. It measures how many new customers return after their first purchase, how much they spend over time, and what that means for acquisition, retention and seasonal planning.

This project is a follow-up to my [Market Basket Analysis](LINK-TO-MBA-REPO), which looked at *what* customers buy together. This one looks at *whether* customers come back.

**Author:** Eugene Gitonga
**Tools:** Python, pandas, numpy, matplotlib, seaborn
**Notebook:** [`cohort\\\_analysis.ipynb`](./cohort_analysis.ipynb) 

\---

## Business Questions

1. How strong is overall customer retention?
2. Does retention differ between cohorts of customers who joined in different months?
3. How much do customers spend over time, and how does that differ between new and established customers?
4. What should the business do with these patterns: when to market, who to protect and where retention drops?

## What Is Cohort Analysis?

A cohort is a group of customers who share a starting point. Here, the starting point is the month of a customer's first purchase. Each cohort is then followed over the months that follow to see how many customers buy again and how much they spend. Looking at all customers together hides these differences: a business can show healthy monthly sales while losing most of its new customers after one order, because a steady flow of new customers replaces them.

## Dataset

Transaction-level records from a UK-based online gift retailer. Each row is a line item on an invoice: invoice number and date, product code and description, quantity, unit price, customer ID and country.

* **Scope:** UK customers only, 1 December 2010 to 30 November 2011
* **Source:** Online Retail dataset  https://www.kaggle.com/datasets/thedevastator/online-retail-sales-and-customer-data

## Approach

1. **Cleaning**

   * Removed rows with a missing customer ID (a customer can't be followed over time without one)
   * Removed duplicate rows
   * Kept UK orders only, so the cohorts match the market basket analysis
   * Excluded December 2011, because the data ends on 9 December and a partial month would understate retention and spend in the last cell of every cohort
   * Created a `Revenue` column (`Quantity × UnitPrice`)
2. **Exploratory checks:** monthly transactions, active customers and revenue; new versus returning customers per month.
3. **Cohort assignment:** each customer's cohort is the month of their first purchase. `CohortIndex` counts the months since that first purchase (1 = the first month).
4. **Cohort tables and heatmaps**

   * Active customers by cohort and month
   * Retention rate (% of the cohort active in each month)
   * Average spend per active customer
   * Cumulative spend per acquired customer (a simple lifetime-value view)



\## Key Findings

\*\*1. Sales are strongly seasonal, with a sharp autumn peak.\*\*
Monthly revenue sits at roughly £350k to £540k from December to August, then jumps to about £790k in September, £810k in October and £970k in November. September to November account for 37.9% of the year's revenue.

\*\*2. Most new customers buy once, and those who return keep returning.\*\*
About 20% of new customers (the average across the 2011 cohorts, range 15 to 24%) buy again in their second month. After that, retention doesn't keep falling. It stays mostly between about 15 and 33%. This suggests a loyal core of periodic buyers plus a large group of one-time buyers.

\*\*3. November pulls customers back across every cohort.\*\*
The November cell is the brightest for every cohort (24 to 50%, against about 20 to 25% in most other months). Customers who had gone quiet return for the Christmas season, so month-to-month retention partly reflects seasonal buying and not only who has stayed.

\*\*4. Acquisition slowed in summer, and the business leaned on returning customers.\*\*
New customers per month fell from 419 in March to 141 in August, then recovered to 276 to 323 in September to November. Returning customers made up 80.3% of active customers in November.

\*\*5. Established customers are more loyal and spend more.\*\*
Customers already active in December 2010 retained at 32 to 40% (50% in November) and spent £600 to £1,170 per active customer. New customers (February to November cohorts) retained at about 20% and spent £360 to £500 in their first month. At month 6, the December 2010 group had spent £1,900 per customer, against £1,351 for the January cohort and £767 to £933 for the February to June cohorts.

\*\*6. A new customer's value builds slowly.\*\*
A new customer spends about £400 in their first month. By month 6, cumulative spend is typically £770 to £930, roughly double the first month.

\*\*7. Customers acquired just before the peak are worth more, sooner.\*\*
The August cohort had spent £991 per customer by month 4 (November), against £568 to £705 for February to July cohorts at the same age. Part of this is timing, because the August cohort's fourth month was the November peak. The cohort is also small (about 31 to 34 active customers a month), so treat it as a pointer.

## Recommendations

1. \*\*Create a first-30-days programme.\*\* About 80% of new customers don't return after their first month. A follow-up two to three weeks after the first order, such as a reorder reminder, a bundle suggestion or a small second-order incentive, targets the biggest drop. The baseline to beat is about 20% month-2 retention.
2. \*\*Prepare for autumn from August.\*\* Stock seasonal ranges early and run a win-back campaign for quiet customers in late August and early September, since many return in the autumn peak.
3. \*\*Test acquiring customers in August to October.\*\* Customers acquired just before the peak reached higher spend sooner, and acquisition was weakest in summer. Run a small test before shifting budget.
4. \*\*Protect the loyal core.\*\* Established customers spend roughly twice as much per active month and return far more often. Identify them (an RFM segmentation is a natural next step) and prioritise their stock availability and service.
5. \*\*Judge cohorts by the same calendar months,\*\* so the November bump isn't mistaken for improved loyalty.

## Limitations

\* \*\*Only 12 months of data,\*\* so seasonality can't be separated from trend.
\* \*\*The December 2010 group isn't a true new-customer cohort.\*\* It includes every customer active that month, including long-standing ones. The January cohort may also include customers who bought before December 2010, so early-2011 new-customer counts are probably overstated.
\* \*\*Small cohorts\*\* (141 to 419 customers), so differences of a few percentage points may be noise.
\* \*\*Retention counts any purchase in a month,\*\* so customers who buy every second or third month appear to "leave" and "return".
\* \*\*Averages are affected by large wholesale-style buyers.\*\*
\* \*\*Association, not causation:\*\* the analysis describes behaviour and doesn't prove what drives it.

## Next Steps

\* \*\*Product-category cohort analysis\*\* (separate notebook): group customers by the category of their first purchase and compare retention and spend, linking this project to the market basket analysis
\* RFM segmentation to identify the loyal core
\* Revenue-based retention alongside customer retention
\* Repeat with a second year of data to separate seasonality from trend

## How to Run

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook cohort\\\_analysis.ipynb
```


## Contact

Eugene Gitonga
Portfolio: https://datascienceportfol.io/eugeneigitonga
X: https://x.com/GITONGAeugene

