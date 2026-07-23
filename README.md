# Feature Engineering & Transformation — Internship Task (Week 4)

Engineer new features and apply transformations to a raw sales dataset to improve downstream ML model quality — covering encoding, scaling, skew correction, and feature creation end to end.

## Overview

This project builds a complete feature engineering pipeline on a synthetic e-commerce sales dataset (500 orders). It takes 10 raw columns and produces 26 model-ready features by handling missing values, extracting date/time signal, engineering interaction and domain-driven features, correcting skewed distributions, encoding categorical variables, and scaling numeric variables.

## Concepts Covered

- **Encoding:** One-Hot, Target, Ordinal
- **Scaling:** StandardScaler, MinMaxScaler, RobustScaler
- **Transforms:** Log Transform, Box-Cox Transform
- **Feature Creation:** Interaction features, domain-driven business rules
- **Date/Time Features:** Year, month, day, day-of-week, weekend flag, quarter, recency

## Tools & Libraries

- `pandas`
- `scikit-learn`
- `category_encoders`
- `feature-engine`

## Project Structure

```
.
├── sales_data.csv                       # raw synthetic dataset (input)
├── engineered_sales_data.csv            # final transformed dataset (output)
├── feature_engineering_pipeline.py      # standalone Python pipeline script
├── feature_engineering_colab.ipynb      # Google Colab notebook version
├── Week4_Feature_Engineering_Report.docx# written report
└── README.md
```

## How to Run

### Option 1 — Python script

```bash
pip install pandas scikit-learn category_encoders feature-engine
python feature_engineering_pipeline.py
```

Produces `engineered_sales_data.csv` in the same directory.

### Option 2 — Google Colab

1. Open `feature_engineering_colab.ipynb` in Google Colab.
2. Run all cells (**Runtime → Run all**).
3. The notebook installs its own dependencies and generates the dataset, so no upload is needed.

## Pipeline Steps

1. **Load & impute** — median imputation on `delivery_days` and `customer_rating`
2. **Date/time features** — decompose `order_date` into year, month, day, day-of-week, weekend flag, quarter, and days since first order
3. **Interaction & domain features** — `gross_amount`, `net_amount`, `discount_amount`, `price_per_delivery_day`, `is_fast_delivery`, `is_high_value_order`
4. **Outlier capping** — IQR-based Winsorizer on skewed monetary/delivery columns
5. **Transforms** — log transform on `gross_amount`/`net_amount`, Box-Cox on `unit_price`
6. **Encoding** — One-Hot on `payment_method`, Target encoding on `city`, Ordinal on `product_category`
7. **Scaling** — StandardScaler, MinMaxScaler, RobustScaler applied by column distribution

## Result

| | Raw | Engineered |
|---|---|---|
| Rows | 500 | 500 |
| Columns | 10 | 26 |
| Missing values | 25 | 0 |

## Author

Umar — BS Computer Science, UET Mardan
