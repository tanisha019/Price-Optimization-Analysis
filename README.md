# Price Optimization Analysis Using Regression Models

## Overview
This project focuses on identifying revenue-maximizing pricing strategies using historical retail sales data. By applying regression-based demand modeling, the analysis estimates price elasticity across multiple product categories and evaluates how pricing decisions influence revenue.

Rather than treating pricing as a one-size-fits-all problem, the project adopts a **category-level approach**, recognizing that customer price sensitivity varies significantly across product types. The goal is to provide **interpretable, data-driven pricing insights** that are both statistically sound and practically actionable.

---

## Objectives
- Estimate **price elasticity of demand** for different product categories  
- Identify **revenue-maximizing price levels or ranges**  
- Compare pricing behavior across categories  
- Translate statistical results into **business-ready recommendations**  

---

## Dataset
The analysis uses a publicly available retail pricing dataset containing monthly aggregated sales data.

### Key variables used:
- `unit_price` – Average selling price per unit  
- `qty` – Quantity sold  
- `total_price` – Total revenue  
- `product_category_name` – Product category identifier  
- Time features (month, year)

Additional variables such as competitor prices and product attributes were present but not explicitly modeled to maintain focus on **own-price elasticity** and interpretability.

---

## Data Quality & Preprocessing

### Missing Values
- A complete missing value audit was performed.
- **No missing values** were found in the dataset.

### Outlier Analysis
- Outliers were identified using the **Interquartile Range (IQR)** method for:
  - Quantity sold
  - Unit price
  - Total revenue
- Approximately **6–7%** of observations were flagged as outliers.

#### Outlier Handling Strategy
- Outliers were **retained**, as they likely represent valid business scenarios such as:
  - Premium-priced products
  - Bulk purchases
- Negative IQR bounds arise from the mathematical formulation of the method and **do not indicate invalid data values**.
- To control the influence of extreme values without discarding information, **logarithmic transformations** were applied in demand models.

---

## Methodology

### Modeling Approach
- Analysis was conducted **separately for each product category** to avoid mixing heterogeneous demand behaviors.
- The following models were evaluated:
  1. **Linear regression** (baseline comparison)
  2. **Log-log regression** (primary model)
  3. **Polynomial regression** (used selectively for robustness checks)

### Elasticity Estimation
The primary model uses a log-log specification:

\[
\ln(Q) = \beta_0 + \beta_1 \ln(P)
\]

Where:
- \( \beta_1 \) represents **price elasticity of demand**
- This form allows direct interpretation of elasticity and reduces sensitivity to extreme values.

---

## Revenue Optimization
Revenue was simulated using:

\[
Revenue = Price \times Predicted\ Quantity
\]

For each category:
- Revenue was evaluated across the **observed historical price range**
- The price that maximized simulated revenue was identified
- When the maximum occurred at the upper bound of the range, results were interpreted as **pricing headroom**, not a precise global optimum

This approach avoids extrapolation beyond available data.

---

## Categories Analyzed
- `garden_tools`
- `health_beauty`
- `watches_gifts`
- `bed_bath_table`

Each category was analyzed independently using the same methodology to ensure consistency.

---

## Key Findings

### Summary of Results

| Category          | Elasticity | Demand Behavior        | Pricing Insight |
|-------------------|------------|------------------------|-----------------|
| garden_tools      | ≈ -0.80    | Inelastic              | Pricing headroom; gradual increases feasible |
| health_beauty     | ≈ -0.14    | Price-insensitive      | Demand driven by non-price factors |
| watches_gifts     | ≈ -0.32    | Weak sensitivity       | Cautious pricing; avoid aggressive discounting |
| bed_bath_table    | ≈ -0.89    | Inelastic              | 8–12% revenue uplift potential |

---

## Visual Analysis
Two key visualizations support the quantitative results:
1. **Log Price vs Log Quantity scatter plots**
   - Explain low R² values
   - Show that price is not the sole driver of demand
2. **Revenue vs Price curves**
   - Clearly illustrate revenue-maximizing regions
   - Provide intuitive justification for pricing recommendations

---

## Business Recommendations
- Use **category-specific pricing strategies** instead of uniform price adjustments
- Implement **controlled price increases** in inelastic categories
- Avoid over-reliance on discounting in price-insensitive categories
- Combine pricing decisions with **non-price levers** such as branding and assortment optimization
- Validate findings with controlled pricing experiments where feasible

---

## Limitations
- The analysis is based on **observational data** and does not establish causality
- Competitive reactions and promotional effects were not explicitly modeled
- Elasticity estimates reflect historical behavior and may change over time

---

## Tools & Technologies
- **Python**
- **Pandas, NumPy**
- **Statsmodels**
- **Matplotlib**
- **Jupyter Notebook**

---

## Project Structure
