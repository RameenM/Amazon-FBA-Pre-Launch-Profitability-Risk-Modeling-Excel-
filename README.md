# Amazon FBA Pre-Launch Profitability & Risk Modeling (Excel)

## Project Overview and Objective

This project is a pre-launch Amazon FBA financial modeling system built entirely in Excel. The objective is to evaluate whether a product is financially viable before capital is deployed and to understand how profitability responds to changes in sales volume, fees, and costs.

The core business question addressed is:

> Are we making money safely, and what happens if conditions change?

Rather than prioritizing dashboards or visualization, the model focuses on:
- Accurate cost attribution
- SKU-level unit economics
- Risk-aware decision making
- Transparent and auditable assumptions

The model simulates an early-stage Amazon FBA launch for a spice cabinet product with two variants:
- SPICE-2T (2-Tier)
- SPICE-3T (3-Tier)

---

## Data Sources and Assumptions

This project combines estimated market data, supplier pricing, and documented assumptions to simulate a realistic pre-launch scenario.

External reference sources include:
- Amazon product listings (pricing, weight, SKU differentiation)
- Alibaba supplier listings (manufacturing cost references)
- Helium 10 FBA Calculator (Amazon fee estimates)
- Public Amazon referral fee schedules for the Kitchen category

Where direct data was unavailable, conservative estimates were used and explicitly documented.

---

## Model Structure and Sheet Design

### Orders_Raw Sheet – Base Input Layer

The orders_raw sheet represents simulated order-level sales activity structured to mirror Amazon order exports. It intentionally contains no complex logic and serves as the foundation for all downstream calculations.

Key fields include:
- order_id: manually generated transaction identifier
- date: simulated 30-day launch window
- sku: product variant identifier
- units: simulated daily sales volume
- sale_price: observed Amazon listing price
- revenue (derived)

Revenue calculation: revenue = units * sale_price

Raw order data alone does not indicate profitability. This sheet preserves separation between data and logic and supports downstream validation.

---

### Product_Costs Sheet – Landed Cost Modeling

The product_costs sheet captures all non-Amazon per-unit costs required to bring inventory into Amazon fulfillment.

Cost components include:
- Supplier cost  
  - SPICE-3T: direct Alibaba reference ($7.71)  
  - SPICE-2T: proportionally derived
- Shipping cost derived from product weight
- Packaging cost fixed at $1.00 per unit
- Landed unit cost (derived)

Landed unit cost calculation: supplier_cost + shipping_cost + packaging_cost

Supplier price alone understates true cost. Landed cost reflects actual capital exposure per unit.

---

### Fee_Lookup Sheet – Amazon Fee Reference Table

The fee_lookup sheet centralizes Amazon platform fees to avoid hard-coded assumptions.

Key fields include:
- fee_type (Referral, Fulfillment, Storage)
- fee_method (percentage or fixed)
- fee_value
- applies_to
- notes

Referral fee calculation: sale_price * referral_rate

Fulfillment and storage fees are applied via SKU-based lookups.

---

### Processed_Orders Sheet – Financial Truth Layer

This is the core analytical layer of the model. It combines raw sales data, landed costs, and Amazon fees to produce order-level profitability.

Key calculations include:
- Revenue
- Total Amazon fees
- Total cost
- Net profit = revenue - total_cost
- Profit margin = net_profit / revenue

This layer enables order-level validation, SKU-level comparison, and loss detection.

---

## SKU-Level Profitability Summary

A pivot table aggregates order-level results into a SKU-level summary suitable for decision-making.

Metrics included:
- Total revenue
- Total cost
- Net profit
- Average profit margin

Key insights:
- SPICE-3T shows higher total profit and higher margins (approximately 40 percent or higher)
- SPICE-2T remains profitable with lower margins (approximately 30 percent or higher)
- Higher per-unit costs for SPICE-3T are offset by stronger contribution margins

---

## Data Validation – Revenue Reconciliation

Revenue was independently calculated at multiple stages of the model to ensure consistency.

Validation steps:
- Revenue calculated at the raw order level
- Compared against revenue in processed_orders
- Discrepancy identified due to numeric fields stored as text
- Corrected and revalidated

Final result:
- Raw revenue equals processed revenue
- Difference equals zero
- Status: PASS

This confirms analytical integrity.

---

## Forecasting and Sensitivity Analysis

The model evaluates short-term profitability sensitivity without producing speculative demand forecasts.

Methodology:
- Baseline: average daily net profit scaled to 30 days
- Downside scenario: minus 10 percent demand
- Upside scenario: plus 10 percent demand
- All prices, fees, and costs held constant

Key results:
- SPICE-3T exhibits higher profit variability
- SPICE-2T shows lower downside exposure
- Profit sensitivity scales proportionally with baseline margins

---

## Limitations and Scope

This project is intentionally conservative and subject to known limitations:
- Sales data is simulated
- Advertising spend is excluded
- Returns and refunds are not modeled
- Storage fees are simplified
- Supplier pricing is estimated for one SKU
- Competitive dynamics are not explicitly modeled

These limitations are acceptable because the goal is pre-launch financial validation rather than post-launch accounting.

---

## Conclusion and SKU Recommendation

The model demonstrates positive profitability under baseline assumptions and remains profitable under moderate downside scenarios. Profitability is driven by unit economics rather than aggressive volume assumptions.

Recommended initial SKU:
- SPICE-2T (2-Tier)

Rationale:
- Lower landed unit cost
- Reduced upfront capital exposure
- Stable margins
- Lower liquidation risk during early testing

SPICE-3T is better suited for scaling after demand validation due to higher margins and greater sensitivity to demand fluctuations.

---

## Key Takeaway

This project demonstrates how Excel-based financial modeling can support disciplined, risk-aware Amazon FBA decision-making by emphasizing transparent assumptions, unit economics, and sensitivity analysis.

