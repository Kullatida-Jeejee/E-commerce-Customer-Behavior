E-Commerce Customer Behavior Analysis 🛒
This repository contains a Statistical Inference and Regression Modeling project based on the E-Commerce Customer Behavior Dataset from Kaggle.
The goal of this project is to investigate the relationship between customer characteristics and Total Spend, identify the most influential predictors of customer expenditure, and build a reliable regression model that provides actionable insights for e-commerce decision-making.

📂 Repository Contents
ecommerce_analysis.ipynb: The main Jupyter Notebook containing all Python code, data cleansing steps, EDA visualizations, hypothesis testing, regression modeling, and diagnostic checks.
E-commerce Customer Behavior - Sheet1.csv: The raw dataset containing 350 customer records with demographic and transactional features (Age, Gender, City, Membership Type, Total Spend, Items Purchased, Average Rating, Discount Applied, Days Since Last Purchase, Satisfaction Level).
README.md: Project documentation and setup instructions.

🚀 How to Open and Run the Project
This project is designed to be fully reproducible and runs seamlessly in the cloud using Google Colab. You do not need to install Python, download any files, or configure a local environment.
Step 1: Open the Notebook by clicking the Colab badge below to launch it directly in your browser.
Step 2: Run the Code

Once inside Google Colab, go to the top menu and click Runtime > Run all.
Zero Setup Required: The notebook is programmed to automatically fetch the dataset directly from this GitHub repository using its Raw URL. You do not need to manually upload the dataset to Colab.

📊 What the Notebook Does
The .ipynb file is structured as an end-to-end statistical modeling report, walking through the following phases:
1. Data Cleansing & Preprocessing
Raw e-commerce data requires careful encoding before regression. The notebook demonstrates data preparation by:
Dropping non-predictive identifiers (Customer ID) and removing rows with missing values, yielding a working dataset of 350 observations.
Label-encoding binary variables (Gender: Male = 1, Female = 0; Discount Applied: True = 1, False = 0).
Ordinally encoding ranked categorical variables (Membership Type: Gold = 3, Silver = 2, Bronze = 1; Satisfaction Level: Satisfied = 2, Neutral = 1, Unsatisfied = 0).
One-hot encoding the City variable using pd.get_dummies with drop_first=True to avoid the dummy variable trap.

2. Exploratory Data Analysis (EDA)
Generates professional visualizations using matplotlib and seaborn to characterize the dataset:
- Distribution Analysis: Histograms reveal that Total Spend is approximately normally distributed, while Age, Items Purchased, Average Rating, and Days Since Last Purchase show roughly uniform distributions — indicating a well-balanced sample.
- Relationship Exploration: Scatterplots of each continuous predictor against Total Spend reveal a strong positive linear pattern for Items Purchased, a weak trend for Age, and no discernible pattern for Average Rating or Days Since Last Purchase.
Correlation Heatmap: Confirms Items Purchased as the dominant predictor (r = 0.89 with Total Spend), with no predictor pair exceeding r = 0.9.

3. Statistical Inference
Applies formal inference techniques to validate observed patterns:
Pearson Correlation Hypothesis Test: A two-tailed test on Items Purchased vs. Total Spend yields r ≈ 0.97 with p ≈ 0.0000, providing overwhelming evidence to reject the null hypothesis of no correlation.
95% Confidence Interval for Mean Total Spend: Constructed using the t-distribution to quantify the precision of the sample mean estimate.

4. Regression Modeling
Builds and compares two regression models:
- Simple Linear Regression (Items Purchased → Total Spend): Achieves R² = 0.945, with each additional item increasing Total Spend by approximately $84.82.
- Multiple Linear Regression (all predictors): Initially flags severe multicollinearity, where Membership Type, Discount Applied, and Satisfaction Level produce infinite VIF values because they are deterministically linked in the dataset (e.g., every Bronze member receives a discount and is recorded as Unsatisfied).
Iterative VIF Reduction: Drops the highest-VIF predictor one at a time until all remaining VIFs fall below 5. The final model retains five predictors — Age, Days Since Last Purchase, City_Houston, City_New York, and City_San Francisco — and achieves R² = 0.9907.

5. Model Evaluation & Diagnostics
Validates regression assumptions through a comprehensive diagnostic suite:
Residuals vs Fitted, Q-Q Plot, Cook's Distance, and Leverage vs Studentized Residuals plots assess linearity, normality, and influence.
Outlier Investigation: Identifies 19 influential points and inspects extreme cases that may represent a distinct customer segment not captured by the retained predictors.
Sensitivity Check: Refits the model excluding influential points; R² changes only marginally (0.9907 → 0.9938) and coefficients remain stable, confirming robustness.
Shapiro–Wilk Normality Test on residuals, with discussion of the Central Limit Theorem given the large sample size (n = 348).

💡 Key Insights

Cart-size maximization through bundling and product recommendations is the strongest supported revenue driver, since Items Purchased alone explains 94.5% of the variance in Total Spend.
Geographic segmentation matters — San Francisco customers spend significantly more than the reference group (Chicago), suggesting city-level marketing strategies.
Recency drives spend — each additional day since last purchase reduces Total Spend by approximately $5.66, supporting re-engagement campaigns for lapsed customers.

⚠️ Limitations
Small sample size (n = 348), severe multicollinearity among encoded categorical variables that prevented their inclusion in the final multiple regression, cross-sectional design that prevents causal inference, and ordinal encoding assumptions for Membership Type and Satisfaction Level.
