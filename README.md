# Dominos Pizza Sales Analysis and Forecasting

This project analyzes pizza sales data and forecasts future sales to optimize inventory management.

## Data Loading and Cleaning

The project starts by loading two CSV files: `sales.csv` and `Pizza_ingredients.csv`. Missing values in both datasets are identified and handled using appropriate methods, primarily by filling missing values based on related columns (`pizza_name`, `pizza_size`, `pizza_name_id`).

## Feature Engineering

New features are created from the `order_date` and `order_time` columns in the `sales.csv` data to facilitate time-series analysis and machine learning models. These include:

- `month`
- `year`
- `day_of_week`
- `week`
- `quarter`
- `hour`

A combined `datetime` column is also created.

## Exploratory Data Analysis (EDA)

The EDA section explores the sales data through various visualizations:

- **Outlier Analysis**: Box plots are used to visualize the distribution of `unit_price` and `total_price` and identify potential outliers.
- **Bar Plots**: Bar charts show the distribution of pizza sales by size and category. A stacked bar chart further breaks down sales by size and category.
- **Pizza Sales by Name**: A bar plot displays the total quantity sold for each pizza name, colored by pizza category.
- **Line Plots**:
    - **Daily Sales**: A line plot shows the total number of pizzas sold each day, with missing dates filled using interpolation.
    - **Monthly Sales**: A line plot illustrates the total pizza sales per month, with values annotated on the plot.
    - **Weekly Sales**: A line plot displays the total pizza sales per week.
    - **Daily Sales for First 3 Months**: A line plot with scatter points colored by the day of the week shows the daily sales trend for the first three months.
    - **Hourly Sales**: A line plot visualizes the total pizza sales per hour to identify peak sales periods.
- **Sales by Day of the Week**: Bar plots show the total quantity sold for each day of the week. A box plot further analyzes the distribution of daily sales by quarter, grouped by the day of the week.

## Time Series Analysis

- **Seasonal Decomposition**: The daily sales time series is decomposed into trend, seasonal, and residual components to understand the underlying patterns.
- **ADF Test**: The Augmented Dickey-Fuller test is performed to check for stationarity in the daily sales time series. The results indicate that the series is likely stationary.
- **Autocorrelation Plots (ACF and PACF)**: ACF and PACF plots are used to identify potential parameters for ARIMA models.

## Modeling and Forecasting

Several models are implemented to forecast pizza sales:

- **Random Forest**
- **XGBoost**
- **Prophet**
- **ARIMA**

Each model is trained and evaluated on individual pizza sales time series grouped by `pizza_name_id`. Feature engineering, including lag values, is applied for the tree-based models (Random Forest and XGBoost).

The performance of each model is evaluated using the Mean Absolute Percentage Error (MAPE).

- Random Forest MAPE: 0.6529
- XGBoost MAPE: 0.5698
- Prophet MAPE: 0.5375
- ARIMA MAPE: 0.5456

The **Prophet model** achieved the lowest overall MAPE, indicating it is the most accurate model for forecasting in this case.

## Inventory Management

Based on the sales forecasts from the Prophet model for the next week, an inventory sheet is generated. This sheet calculates the required quantity of each pizza ingredient in grams by merging the predicted pizza quantities with the ingredient information from `Pizza_ingredients.csv`. The inventory sheet is then sorted by the required quantity of ingredients in descending order.

This project provides a comprehensive analysis of pizza sales and a data-driven approach to inventory management through time series forecasting.
