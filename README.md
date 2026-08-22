# Decoding Customer Value — D2C Retention Analytics

Customer segmentation and retention analysis for a direct-to-consumer fashion brand (3,900 customers), built with Python, SQL and Power BI.

---

## Key findings

**Top 25% of customers drive 65% of forward annual revenue.** The bottom quartile accounts for 2.2%.

**Value is driven entirely by purchase frequency, not basket size.** Average basket is flat at roughly $60 across every cadence band, while forward annual value spans 51x — $3,067 for weekly buyers versus $60 for annual buyers. Weekly and bi-weekly customers are 42% of the base and 83% of forward revenue.

**The promotional field carries no behavioural signal.** Discount status is perfectly confounded with gender: zero of 1,248 female customers ever received a discount (chi-square = 1382, p < 1e-300; roughly 537 expected under independence). Discounted and full-price customers are otherwise identical on basket, cadence, purchase history, value and satisfaction. The promo axis was dropped from the segmentation and reported as a data artifact rather than a customer behaviour.

**No geographic opportunity exists in this data.** State-level differences in customer value are not statistically distinguishable from random variation (ANOVA p = 0.145 across 50 states).

---

## Method

Loyalty is not a column in the dataset, so it had to be constructed. Two competing definitions were built and tested against each other. Both initial versions failed:

- **Definition A** (cadence + history + full-price status) drew 53.7% women against a 32.0% baseline — the full-price filter was inheriting the gender confound.
- **Definition B** (top value quartile + satisfaction) produced identical concentration with and without its satisfaction filter, and its customers matched the population average on every loyalty-relevant measure.

The surviving definition uses purchase cadence and history only, with no value or discount inputs. It captures 48.4% of forward revenue from 28.9% of customers (1.67x concentration) with a gender mix at baseline.

Three plausible-looking findings were tested and discarded during the analysis: the promo-dependency segments, a 23% basket premium among top customers that turned out to be forced by the definition's own formula, and a geographic opportunity that did not survive an ANOVA.

---

## Segmentation

| Segment | Customers | Share of revenue | Avg annual value |
|---|---|---|---|
| Core Loyal | 13.4% | 34.8% | $2,703 |
| Established | 15.5% | 13.5% | $905 |
| Developing | 49.7% | 48.1% | $1,004 |
| Low Engagement | 21.4% | 3.6% | $175 |

Gender mix (29–34%) and discount rate (42–45%) sit at baseline in every segment, confirming the scheme separates customers on behaviour rather than on the data artifact.

---

## Ideal customer profile

Buys monthly or more often, with 25+ prior purchases. Loyal customers are not distinguishable from the average customer by age (44.8 vs 43.8), basket size ($59.72 vs $59.78, p = 0.94), category preference, or satisfaction. Two attributes separate them: orders per year (29.1 vs 12.7) and purchase history depth (37.2 vs 20.5).

The implication for marketing is to stop building demographic personas and optimise for repeat rate instead.

---

## Stack

- **Python** — cleaning, feature engineering, hypothesis testing (pandas, scipy)
- **SQL** — segmentation queries using CTEs, window functions and star-schema joins (SQLite)
- **Power BI** — four-panel dashboard with DAX measures

---

## Files

| File | Contents |
|---|---|
| `d2c_analysis.ipynb` | Full pipeline — audit, cleaning, feature engineering, segmentation, SQL |
| `d2c_dashboard.pbix` | Power BI dashboard |
| `customers_powerbi.csv` | Cleaned dataset with engineered features |
| `dim_region.csv` | State-to-region dimension table |

---

## Dashboard

<img width="981" height="568" alt="image" src="https://github.com/user-attachments/assets/3a478bac-0e9b-47aa-9cf3-3842781c9946" />

