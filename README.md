## Hi there 👋

Bengaluru Housing Price Prediction Report
**1. Introduction**
This report details the process of predicting housing prices in Bengaluru, India, using a dataset containing various property attributes. The objective is to build and evaluate several machine learning models to determine their effectiveness in accurately forecasting house prices.

**2. Data Overview and Cleaning Summary**
The initial dataset, Bengaluru_House_Data.csv, contained approximately 13,320 rows and 9 columns. Before model building, a comprehensive data cleaning process was performed to handle missing values, inconsistent data formats, and outliers. Key cleaning steps included:

**Missing Values:**

Rows with missing size values were dropped.

Missing values in bath and balcony were imputed with their respective medians.

The society column, which had a high number of missing values and unique categories, was dropped.

**Feature Transformation:**

The size column (e.g., "2 BHK", "4 Bedroom") was converted into a numerical bhk (bedrooms, hall, kitchen) column.

The total_sqft column, which contained ranges and non-standard entries, was converted into a single numerical value (averaging ranges). Rows that could not be converted were dropped.

**Feature Engineering:** A price_per_sqft (price per square foot) feature was created to aid in outlier detection and provide a normalized price indicator.

**Outlier Removal:** Outliers were systematically removed based on:

price_per_sqft (using standard deviation within each location).

Illogical bhk to total_sqft ratios (e.g., less than 300 sqft per BHK).

Excessive number of bathrooms compared to bhk (e.g., more than bhk + 2).

Dimensionality Reduction for location: Locations with very few data points (less than or equal to 10 properties) were grouped into an 'Other' category to manage high cardinality, which is beneficial for one-hot encoding.

**Column Dropping:** The original size and price_per_sqft columns were dropped, as they were either replaced or used for intermediate cleaning steps.

After cleaning, the dataset was transformed using one-hot encoding for categorical features (area_type, availability, location) and then split into training (80%) and testing (20%) sets.

**3. Machine Learning Model Performance**
Three regression models from Scikit-learn were trained and evaluated on the cleaned and preprocessed data. The models' performance was assessed using Mean Squared Error (MSE) and R-squared (R²) score on the test set.

Mean Squared Error (MSE): Measures the average squared difference between estimated values and actual values. Lower MSE indicates better fit.

R-squared (R²): Represents the proportion of the variance in the dependent variable that is predictable from the independent variables. A higher R² (closer to 1) indicates a better fit.

Model

Mean Squared Error (MSE)

R-squared (R²) Score

Linear Regression

2440.9667

0.7570

Decision Tree Regressor

7221.3870

0.2810

Random Forest Regressor

2778.1339

0.7234

Observations:

Linear Regression serves as a baseline, showing an R-squared score of 0.7570, indicating that it explains about 75.7% of the variance in house prices.

Decision Tree Regressor performed less optimally in this run, with a higher MSE (7221.39) and a significantly lower R-squared (0.2810) compared to the other models. This might suggest the default parameters led to overfitting or underfitting, or that the specific data split favored other models for this particular run.

Random Forest Regressor demonstrated a strong performance, with an MSE of 2778.13 and an R-squared of 0.7234. While slightly lower than Linear Regression in this specific run, ensemble models like Random Forests are generally robust and can be further optimized with hyperparameter tuning.

**4. Conclusion and Recommendations**
Based on the updated evaluation metrics, Linear Regression shows the highest R-squared score and lowest Mean Squared Error in this specific run, making it the most suitable model among the tested options for predicting housing prices in this dataset. However, the performance of the Decision Tree and Random Forest Regressors can often be significantly improved with further tuning.
