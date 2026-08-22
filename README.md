\# Decoding Customer Value — D2C Retention Analytics



Customer segmentation and retention analysis for a D2C fashion brand

(3,900 customers). Python → SQL → Power BI.



\## Key findings



\- \*\*Top 25% of customers drive 65% of forward annual revenue.\*\*

\- \*\*Value is driven entirely by purchase frequency, not basket size.\*\*

&#x20; Average basket is flat at \~$60 across every cadence band, while annual

&#x20; value spans 51x (Weekly $3,067 vs Annually $60).

\- \*\*The promotional field carries no behavioural signal.\*\* Discount status

&#x20; is perfectly confounded with gender (chi-square = 1382, p < 1e-300):

&#x20; zero of 1,248 female customers ever received a discount. Discounted and

&#x20; full-price customers are otherwise identical on basket, cadence, history,

&#x20; value and satisfaction. The promo axis was dropped from the segmentation

&#x20; and reported as a data artifact.

\- \*\*No geographic opportunity exists in this data.\*\* State-level value

&#x20; differences are not statistically significant (ANOVA p = 0.145).



\## Method



Loyalty is not a column in the dataset, so it was constructed. Two competing

definitions were built and tested; both initial versions failed (one inherited

the gender confound, one was circular by construction) and were rebuilt. The

surviving definition uses purchase cadence and history only — no value or

discount inputs — and still captures 48.4% of forward revenue from 28.9% of

customers.



\## Stack



\- \*\*Python\*\* — cleaning, feature engineering, hypothesis testing (pandas, scipy)

\- \*\*SQL\*\* — segmentation queries with CTEs, window functions, star-schema joins (SQLite)

\- \*\*Power BI\*\* — four-panel dashboard with DAX measures



\## Files



| File | Contents |

|---|---|

| `d2c\_analysis.ipynb` | Full pipeline: audit, cleaning, features, segmentation, SQL |

| `d2c\_dashboard.pbix` | Power BI dashboard |

| `customers\_powerbi.csv` | Cleaned dataset with engineered features |

| `dim\_region.csv` | State-to-region dimension table |



