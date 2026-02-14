# Chicago Food Inspections: Operational & Risk Analysis

## Project Overview

This project analyzes food inspection data from the City of Chicago to understand inspection volume trends, risk classification distribution, and establishment activity patterns.

Rather than using a random subset, this repository contains the **most recent 20,000 inspection records**, allowing the analysis to focus on current regulatory activity and operational trends.

The objective of this exploratory analysis is to examine how inspection efforts are distributed across time, facility types, and risk categories, and to better understand how the city's food safety monitoring system operates in practice.

---

## Data Source

City of Chicago Data Portal  
https://data.cityofchicago.org/Health-Human-Services/Food-Inspections/4ijn-s7e5/about_data

The dataset contains inspection records for restaurants, schools, grocery stores, mobile food vendors, and other food-related establishments operating within the city.

All original columns are preserved, including detailed violation descriptions.

---

## Dataset Preparation

To ensure the analysis reflects current inspection behaviour, the dataset was restricted to the most recent 20,000 inspections based on `Inspection Date`.

The following code was used:

```python
import pandas as pd

# Load full dataset
df = pd.read_csv("Food_Inspections_20260210.csv")

# Convert Inspection Date to datetime
df["Inspection Date"] = pd.to_datetime(df["Inspection Date"])

# Sort by date (newest first)
df_sorted = df.sort_values("Inspection Date", ascending=False)

# Select latest 20,000 inspections
df_latest_20k = df_sorted.head(20000)

# Save dataset (Violations column preserved)
df_latest_20k.to_csv(
    "chicago_food_inspections_latest_20k.csv",
    index=False
)
