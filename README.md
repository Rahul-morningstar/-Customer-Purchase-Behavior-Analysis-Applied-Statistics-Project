📊 Customer Purchase Behavior Analysis — Applied Statistics Project

Descriptive Statistics | Probability Distributions | Customer Segmentation
A complete end-to-end applied statistics project analyzing customer purchasing patterns to optimize marketing strategy.


📋 Table of Contents

Project Overview
Dataset
Project Structure
Tasks Breakdown

Task 1 — Data Cleaning & Exploration
Task 2 — Descriptive Statistics
Task 3 — Probability Distributions
Task 4 — Insights & Customer Segmentation
Task 5 — Conclusions & Recommendations
Bonus — Law of Large Numbers


Key Findings
Business Recommendations
Technologies Used
How to Run
Output Files


🎯 Project Overview
This project applies descriptive statistics, probability theory, and machine learning-based segmentation to analyze customer information and purchasing behavior. The goal is to:

Identify patterns and trends in customer demographics and spending
Model campaign response rates using probability distributions
Segment customers into actionable marketing groups
Generate data-driven recommendations to improve offer acceptance rates


📁 Dataset
PropertyDetailsSourceGoogle Sheets (publicly shared CSV)Records~2,200 customersFeaturesDemographics, spending by category, purchase channel, campaign responsesTarget VariableResponse — whether a customer accepted the latest marketing offer (binary: 0/1)
Key columns used:
ColumnDescriptionIncomeAnnual household incomeYear_BirthCustomer birth year (used to derive Age)EducationEducation levelMarital_StatusMarital statusMntWines, MntMeatProducts, etc.Amount spent per product category in last 2 yearsNumWebPurchases, NumStorePurchases, etc.Purchases made per channelRecencyDays since last purchaseResponseDid the customer accept the last campaign offer?Dt_CustomerDate of enrollment

📂 Project Structure
📦 Applied-Statistics-Project/
│
├── 📓 Applied_Statistics_Project_Solved.ipynb   ← Main notebook
│
├── 📊 Output Plots/
│   ├── task1_demographics.png                   ← Age, Education, Marital Status distributions
│   ├── task2_boxplots.png                       ← Outlier detection box plots
│   ├── task2_spend_distributions.png            ← Spending histograms by category
│   ├── task3_binomial.png                       ← Binomial distribution — campaign response
│   ├── task3_normal.png                         ← Normal distribution fit — Income & Spending
│   ├── task3_qq.png                             ← Q-Q plots for normality check
│   ├── task4_scatter.png                        ← Income vs Spending, Children vs Spending
│   ├── task4_elbow.png                          ← Elbow method for K-Means
│   ├── task4_segments.png                       ← Customer segment visualization
│   ├── task4_group_spending.png                 ← Spending by Education & Marital Status
│   ├── task5_dashboard.png                      ← Channel effectiveness dashboard
│   ├── task5_radar.png                          ← Spending radar: Responders vs Non-Responders
│   └── bonus_lln.png                            ← Law of Large Numbers simulation
│
└── 📄 README.md

📝 Tasks Breakdown

Task 1 — Data Cleaning & Exploration 🧹
Goal: Prepare a clean, analysis-ready dataset.
Steps Performed:
1.1 Initial Exploration

Checked dataset shape: rows × columns
Reviewed data types for all columns
Identified missing values and duplicate rows

1.2 Handle Missing Values

Income column had ~24 missing values
Imputed with median (robust to outliers): $51,381
Verified zero remaining nulls after imputation

1.3 Fix Data Types & Feature Engineering

Dt_Customer column had ######## (Excel overflow) — replaced with NaN before parsing
Used pd.to_datetime(..., format='mixed', dayfirst=True) for flexible date parsing
Dropped rows where date could not be parsed

1.4 Remove Unrealistic Records

Derived Age = 2024 − Year_Birth
Flagged and removed customers with Age > 100 (data entry errors)

1.5 Derived Features Created
FeatureFormulaAge2024 − Year_BirthTotal_SpendingSum of all 6 product spend columnsTotal_PurchasesSum of all 4 purchase channel columnsTenure_DaysDays from enrollment to Jan 1, 2024Total_ChildrenKidhome + Teenhome
1.6 Demographics Visualizations
Three plots produced:

Age Distribution — histogram with mean & median lines
Education Level — bar chart with counts
Marital Status — pie chart with percentages


Task 2 — Descriptive Statistics 📊
Goal: Summarize data numerically and detect outliers.
Key Variables Analyzed:
Age, Income, Total_Spending, Total_Purchases, MntWines, MntMeatProducts, Recency, Tenure_Days
2.1 Measures of Central Tendency & Dispersion
For each numeric column, computed:
StatisticDescriptionMeanArithmetic averageMedianMiddle value (robust to outliers)ModeMost frequent valueStd DevSpread around the meanVarianceSquared spreadSkewnessAsymmetry of the distributionKurtosisTail heavinessIQRQ3 − Q1 (interquartile range)
2.2 Outlier Detection (IQR Method)

Outliers defined as: values below Q1 − 1.5×IQR or above Q3 + 1.5×IQR
Produced a report showing Outlier Count and % of Dataset for each key variable
Box plots generated for all key variables

2.3 Spending Distribution Histograms
Histograms (with mean line) plotted for all 6 product categories:
MntWines, MntFruits, MntMeatProducts, MntFishProducts, MntSweetProducts, MntGoldProds

Task 3 — Probability Distributions 🎲
Goal: Model real-world events using appropriate probability distributions.

3.1 Binomial Distribution — Campaign Response
Variable: Response (binary: 0 = declined, 1 = accepted)
ParameterValueAcceptance rate p~14.91%Number of trials n100 customersExpected acceptances E[X]~14.91Variance~12.68
Probabilities computed:
EventP(X = k)P(X ≥ k)Exactly 5 acceptcalculatedcalculatedExactly 10 acceptcalculatedcalculatedExactly 15 acceptcalculatedcalculatedExactly 20 acceptcalculatedcalculatedExactly 25 acceptcalculatedcalculated
📊 Binomial PMF bar chart saved as task3_binomial.png

3.2 Normal Distribution — Income & Total Spending
Tested both variables for normality using the Shapiro-Wilk test.
VariableMean (μ)Std Dev (σ)Shapiro p-valueVerdictIncome~$52,247~$25,173< 0.05Not Normal (right-skewed)Total_Spending~$605~$602< 0.05Not Normal (right-skewed)
Probability calculations (Normal approximation):

P(Income < $40,000)
P(Income > $70,000)
P($40K < Income < $80K)
P(within 1 std dev) ≈ 0.6827 (68-95-99.7 rule verification)

3.3 Q-Q Plots
Q-Q plots for both Income and Total_Spending vs. the theoretical Normal distribution — visually confirm deviations from normality.

Task 4 — Insights & Customer Segmentation 📈
Goal: Discover relationships between variables and cluster customers into segments.
4.1 Correlation Analysis
Computed full correlation matrix on all relevant numeric features. Key correlations examined:

Income ↔ Total_Spending
Total_Children ↔ Total_Spending
Recency ↔ Response

4.2 Spending vs. Income & Children
Two plots produced:

Scatter plot: Income vs. Total Spending, colored by Response — reveals that high-income customers who accept offers (red dots) cluster in the upper-right quadrant
Box plot: Total Spending by number of children — shows a clear negative relationship

4.3 K-Means Customer Segmentation
Features used for clustering:
Income, Total_Spending, Total_Purchases, Recency, Age, Total_Children
Process:

Scaled features using StandardScaler
Used the Elbow Method (k = 2 to 8) to find optimal clusters
Chose k = 4 as the optimal number of clusters

Resulting Customer Segments:
SegmentLabelDescription0💰 Budget ShoppersLow income, low spending, price-sensitive1👑 Premium BuyersHigh income, high spending, frequent purchasers2👨‍👩‍👧 Family SaversMid income, children present, deals-focused3🏆 High EarnersHigh income, moderate spending, low recency
Segment profiles include average Response rate per group.
4.4 Spending by Education & Marital Status
Bar charts showing:

Average total spending grouped by Education Level (PhD and Master's spend the most)
Average total spending grouped by Marital Status


Task 5 — Conclusions & Recommendations 🏁
5.1 Channel Effectiveness Dashboard
Three visualizations:

Purchases by channel: Store > Web > Catalog > Deals
Recency distribution: How recently customers made their last purchase
Response rate by web visits: High-frequency web visitors surprisingly show lower conversion rates

5.2 Spending Radar Chart
Compares spending profiles across 6 categories:
CategoryRespondersNon-Responders🍷 WinesMuch higherLower🥩 MeatMuch higherLower🐟 FishSlightly higherLower🍬 SweetsSlightly higherSimilar🍎 FruitsSlightly higherSimilar🥇 GoldSimilarSimilar

Bonus — Law of Large Numbers 🎰
Link: GeoGebra Experiment
Simulation: 5,000 coin flips for three coin biases:
ScenarioTrue Probability (p)Fair Coin0.50Biased Coin0.30Heavily Biased0.75
Result: With very few flips the running mean fluctuates wildly. As the number of flips increases toward 5,000, the running mean converges to the true probability p for all biases — demonstrating the Law of Large Numbers: "More data → closer to the truth."

🔍 Key Findings

Income ↔ Spending: Strong positive correlation (~0.79). Higher-income customers spend significantly more across all categories.
Children ↔ Spending: Negative relationship — households with more children spend less on discretionary categories like wines and meat.
Web Visits ↔ Response: High-web-visit customers have lower offer acceptance rates — they may be comparison shoppers, not converters.
Top Categories Among Responders: Wine and Meat products see ~3× more spending from customers who accept offers vs. those who decline.
Store Dominates Purchase Channels: Store purchases lead all channels in average volume, followed by Web, then Catalog, then Deals.
Education Matters: PhD and Master's-educated customers show the highest average spending across the dataset.


🎯 Business Recommendations
PriorityRecommendation✅ HighTarget high-income, low-web-visit customers — most likely to convert with premium campaigns✅ HighBundle Wine + Meat offers — these are the top categories for responders✅ MediumPrioritize Catalog and Store channels for high-value campaigns✅ MediumCreate family-friendly offers for multi-child households to increase their low engagement rates✅ MediumRe-engage customers with Recency > 60 days using personalized win-back campaigns✅ LowCraft premium, detail-oriented messaging for PhD and Master's-educated customers

🛠 Technologies Used
LibraryPurposepandasData loading, cleaning, manipulationnumpyNumerical computationsmatplotlibBase plottingseabornStatistical visualizationsscipy.statsShapiro-Wilk test, Normal/Binomial distributions, Q-Q plotssklearn.preprocessingFeature scaling (StandardScaler)sklearn.clusterK-Means clusteringgdownDataset loading from Google Drive/Sheets

▶️ How to Run
Option 1 — Google Colab (Recommended)

Upload the .ipynb file to Google Colab
Run all cells top-to-bottom (Runtime → Run all)
The dataset loads automatically from Google Sheets — no manual download needed

Option 2 — Local (Jupyter Notebook)
Prerequisites:
bashpip install pandas numpy matplotlib seaborn scipy scikit-learn gdown
Steps:
bashgit clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
jupyter notebook Applied_Statistics_Project_Solved.ipynb
Then run all cells in order.

Note: The dataset is loaded directly from a public Google Sheet URL — no separate data file is required.


📤 Output Files
All plots are saved to the working directory after running the notebook:
FileTaskDescriptiontask1_demographics.pngTask 1Age, Education, Marital Status distributionstask2_boxplots.pngTask 2Box plots for outlier detectiontask2_spend_distributions.pngTask 2Spending histograms by product categorytask3_binomial.pngTask 3Binomial PMF — campaign response modeltask3_normal.pngTask 3Normal distribution fit for Income & Spendingtask3_qq.pngTask 3Q-Q plots for normality checktask4_scatter.pngTask 4Income vs Spending, Spending vs Childrentask4_elbow.pngTask 4Elbow curve for K-Means cluster selectiontask4_segments.pngTask 4Customer segment scatter + response ratestask4_group_spending.pngTask 4Spending by Education & Marital Statustask5_dashboard.pngTask 5Channel effectiveness dashboardtask5_radar.pngTask 5Radar chart — Responders vs Non-Respondersbonus_lln.pngBonusLaw of Large Numbers coin flip simulation

👤 Author
    Rahul

Applied Statistics 
https://github.com/Rahul-morningstar/

If you find this project useful, feel free to ⭐ star the repository!
