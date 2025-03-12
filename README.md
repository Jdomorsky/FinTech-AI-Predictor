---
# **ML Stock Market Predictor**
---
## **Table of Contents**
---

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)

---
### Project Overview
---

The project is an end-to-end machine learning pipeline designed to predict next-day price movements in the S&P 500. Beginning with historical data sourced from Yahoo Finance, the dataset spans from 1927 but is strategically narrowed to include only data from 1990 onward to focus on modern market trends. In the initial stages, careful data preparation plays a pivotal role: unnecessary columns such as dividends and stock splits are removed, and a target variable is engineered by shifting the closing price by one day. This transformation clearly demarcates whether the market closed higher on the following day, framing the problem as a binary classification task.

At its core, a RandomForestClassifier serves as the baseline predictive model using fundamental features like the open, high, low, close prices, and trading volume. The model is trained on historical segments and then validated through a custom backtesting framework that simulates real-time updates, ensuring that the predictions are always based on the most recent available data. As the project evolves, more nuanced features are introduced—rolling averages and trend indicators computed over multiple horizons provide deeper insights into market momentum and price behavior. These enhancements aim to capture both short-term fluctuations and long-term trends, thereby adapting the model to the inherent complexity of financial time-series data. Although the refined model maintains a modest precision, it illustrates the essential iterative process of model evaluation, feature engineering, and continuous refinement necessary for tackling real-world financial forecasting challenges.

![Graph 1](https://github.com/user-attachments/assets/5c340ad7-33b2-4473-973b-d8c9904af05f)

![Graph 2](https://github.com/user-attachments/assets/ea08475f-d8fe-4c5e-b6a4-e5d4ed1a98bb)

---
### Data Sources
---

The primary data source for this project is Yahoo Finance, accessed through the yfinance Python library. This service provides comprehensive historical market data for the S&P 500 index, including key financial parameters such as opening, high, low, and closing prices, as well as trading volumes. The raw dataset spans from 1927 to the present, but for the purposes of this analysis, we focus on data from 1990 onward to capture more relevant, modern market trends. In preparing the data, we removed extraneous columns like dividends and stock splits to streamline our analysis. Additionally, we engineered new columns such as 'Tomorrow'—by shifting the closing prices—and a binary 'Target' that indicates an upward market movement the following day. This refined dataset not only simplifies the modeling process but also ensures that the inputs are both clean and directly aligned with the predictive goals of the project.

---
### Tools
---

- ***Visual Studio Code (VS Code):***
  - Utilized as the primary Integrated Development Environment (IDE) with Jupyter Notebook extensions for interactive coding and documentation.

- ***Python:***
  - The main programming language used throughout the project.

- ***Jupyter Notebook:***
  - Enabled an interactive environment for iterative data exploration and model building.

- ***yfinance:***
  - Accesses historical stock market data from Yahoo Finance.

- ***pandas:***
  - Handles data manipulation, cleaning, and analysis.

- ***numpy:***
  - Provides numerical computation capabilities essential for data processing.

- ***scikit-learn:***
  - Offers machine learning tools, including the RandomForestClassifier and evaluation metrics like precision_score.

- ***Custom Backtesting Framework:***
  - A set of Python functions designed to simulate trading scenarios by retraining and testing the model on rolling datasets.

---
### Data Cleaning
---

The data cleaning process was critical to ensure that our dataset was suitable for building an effective predictive model. Below is an overview of the cleaning steps applied:

- ***Data Retrieval & Initial Inspection:***
  - Downloaded historical S&P 500 data via the yfinance library, which included records from 1927 to the present.
  - Conducted an initial inspection of the data to familiarize with its structure and contents.

- ***Column Pruning:***
  - Removed extraneous columns such as dividends and stock splits, which were not necessary for the prediction task. This streamlined the dataset and reduced noise.

- ***Feature Engineering – Creating the 'Tomorrow' Column:***
  - Added a new column, Tomorrow, by shifting the closing prices by one day. This column was crucial for linking today's market data with the next day's market performance.

- ***Target Variable Construction:***
  - Constructed a binary Target column to indicate whether the market's closing price would rise the next day. Specifically, if Tomorrow's closing price was greater than today's Close, the target was set to 1; otherwise, it was set to 0.

- ***Date Range Filtering:***
  - Focused the analysis on more recent and relevant market data by filtering the dataset to include only records from January 1, 1990 onward. This step helped in avoiding the noise and structural differences present in the earlier part of the century.

- ***Handling Missing Values:***
  - After further feature engineering (including the introduction of rolling averages and other derived metrics), any rows with missing values were removed to ensure the dataset's integrity for model training.

Each of these steps was performed incrementally, ensuring that the data fed into the model was clean, consistent, and aligned with our predictive objectives.

---
### Exploratory Data Analysis
---


During the exploratory data analysis phase, the focus was on understanding the historical behavior of the S&P 500 and unearthing patterns that could inform the predictive modeling process. Initially, the data was visualized using line graphs to trace the trajectory of the S&P 500’s closing prices over time. This visualization revealed long-term trends, periods of steady growth, and moments of considerable volatility, which set the stage for deeper analysis.

Key descriptive statistics were computed to gauge the central tendencies and variability within the dataset. This helped in identifying outliers and understanding the distribution of important variables such as the opening, high, low, and closing prices, as well as the trading volume. By looking at these statistics, it was possible to confirm that the cleaned data was well-prepared for further analysis, ensuring consistency and reliability in the insights being derived.

In addition to understanding the basic price movements, special attention was given to the newly engineered features. The creation of the Tomorrow column and the corresponding binary Target allowed for an immediate visual inspection of the relationship between today’s data and the market's movement the following day. Plots comparing the actual Target values with the model predictions provided a preliminary validation of the feature engineering approach. This step confirmed that the engineered features captured meaningful patterns that could potentially drive predictive performance.

Furthermore, additional visualizations such as rolling averages and trend indicator plots were constructed. These plots were instrumental in highlighting short- and long-term market behaviors by smoothing out the daily noise and emphasizing overarching trends. The insights gained from these visual analyses not only provided confidence in the data transformations made but also laid the foundation for the subsequent steps of model training and backtesting.


---
### Data Analysis
---

![Code Snip 1](https://github.com/user-attachments/assets/03fdfe38-cd66-4c05-a0e1-92cd5bb4f77c)

![Code Snip 2](https://github.com/user-attachments/assets/eef501ef-10f7-44ca-839a-23f6ac18b786)

![Code Snip 3](https://github.com/user-attachments/assets/c5a1289a-9142-4a04-9a87-59fec06e35d0)

---
### Results
---

The project yielded promising results, showcasing the iterative improvements achieved through feature engineering and dynamic backtesting. Initially, a baseline model built with fundamental price and volume predictors reached a precision of around 53%, providing a modest starting point in the challenging arena of stock market prediction.

By incorporating advanced features—such as rolling averages and trend indicators calculated over varying horizons—the model was enhanced to capture both short-term fluctuations and longer-term trends. This additional layer of feature engineering, combined with a refined backtesting framework that simulates real-time updates, resulted in a measurable improvement. After applying a carefully chosen probability threshold (0.6) to convert the model's output into binary predictions, the final precision score improved to approximately 55.41%.

Key observations from the results include:

- Improved Precision: With the refined feature set and dynamic retraining strategy, the precision score rose from about 53% to 55.41%. This indicates that when the model predicts an upward movement, it is correct more than half the time—a notable improvement in a complex, noisy prediction task.

- Robust Backtesting Performance: The backtesting framework, which involved retraining the model on a rolling window of historical data, demonstrated that the model's predictive power remains reasonably consistent across different periods. This approach validates the model's potential applicability in real-world market conditions.

- Feature Significance: The introduction of rolling metrics—such as close ratios and trend indicators—proved beneficial by adding valuable contextual data. These engineered features allowed the model to better understand market momentum, providing insights that go beyond surface-level price movements.

While a precision of around 55.41% leaves room for further optimization, it underscores the potential of machine learning methods in financial forecasting. Future work may involve experimenting with different thresholds, trying alternative modeling techniques, or incorporating additional market indicators to further refine the model.

These results not only affirm the soundness of the methodology but also highlight the iterative nature of model development where each enhancement, even incremental, contributes meaningfully to tackling real-world forecasting challenges.


---
### Recommendations
---

Based on the results and insights derived from this project, several recommendations can be made for further refinement and exploration:

- Enhance Feature Engineering: While the current model leverages rolling averages and trend indicators, consider incorporating additional technical indicators such as moving averages (SMA, EMA), Relative Strength Index (RSI), or MACD. Integrating fundamentals like volatility measures or even sentiment analysis from financial news could further enrich the model’s context.

- Optimize Model Parameters: Experiment with different hyperparameters using automated methods like grid search or Bayesian optimization. Exploring a wider range of values for the number of estimators, minimum samples split, or even trying other algorithms (e.g., Gradient Boosting Machines, XGBoost) may yield improved precision and overall model performance.

- Refine Prediction Thresholds: The current threshold of 0.6 for converting probability outputs into binary predictions works well, but it might not be optimal. An investigation using precision-recall curves or ROC analysis could help determine a more balanced threshold, especially when considering trade-offs between precision and recall.

- Expand Backtesting Strategies: The rolling window backtesting framework is a robust start. Future work could incorporate transaction costs, slippage, or more realistic market conditions to simulate a live trading environment. Additionally, testing the model across various market regimes (e.g., during high volatility vs. stable periods) can provide a more comprehensive evaluation of its robustness.

- Consider Ensemble Techniques: Combining predictions from multiple models (e.g., by stacking or blending different classifiers) can help mitigate overfitting and capture diverse market patterns. Ensembles often lead to more stable and reliable predictions in complex, noisy environments like the stock market.

- Incorporate Cross-Validation: Rather than relying solely on a train-test split and rolling window backtesting, consider implementing cross-validation techniques tailored for time-series data. This approach will offer further insights into the model’s generalizability across different segments of the dataset.

Implementing these recommendations can pave the way for a more sophisticated and robust predictive framework, better suited to navigate the complexities of financial market forecasting.
---
### Limitations
---

Despite the promising results, several limitations must be acknowledged. First, the predictive model achieves a precision of roughly 55%, indicating that there is significant room for improvement. The inherent complexity and volatility of financial markets mean that even advanced models can struggle to capture all the nuances influencing market movements. This precision level reflects the difficulty of forecasting next-day trends in the S&P 500, where many external factors—such as macroeconomic events and unexpected market shifts—remain unaccounted for.

Another key limitation is the reliance on historical data from Yahoo Finance, which, while comprehensive, may not fully capture the idiosyncrasies or anomalies of current market conditions. The period selected for analysis (from 1990 onward) provides a modern view but may still introduce biases formed by past market dynamics that do not necessarily hold true in the future. Moreover, the data cleaning process involves dropping rows with missing values, which can lead to a loss of potentially valuable information and may inadvertently skew the dataset.

The choice to use a binary classification framework, wherein the model predicts only an upward or downward movement, also simplifies the complexity of market behavior. Such a binary approach does not capture the magnitude of price changes or indicate the volatility inherent in market movements. Additionally, while the backtesting framework simulates an evolving market scenario through rolling windows, it does not fully replicate a live trading environment where factors like transaction costs, slippage, and market liquidity play a critical role.

Finally, the model's dependence on a fixed threshold for probability conversion may not be optimal across all market conditions. The use of a single threshold might lead to misclassifications in certain periods, suggesting that adaptive thresholding or more granular risk measures could be beneficial. Future work should address these limitations by incorporating more robust data handling, considering external economic indicators, and exploring alternative modeling techniques to better navigate the unpredictable nature of financial markets.


---
### References
---

- [***Visual Studio Code (VS Code):***](https://code.visualstudio.com/) IDE used with the Jupyter Notebook extensions for interactive analysis.

- [***Jupyter Notebook:***](https://jupyter.org/) Interactive computing environment that facilitated exploratory data analysis.

- [***Python:***](https://www.python.org/) The programming language used for this project.

- [***Yahoo Finance:***](https://finance.yahoo.com/) Data source for historical market data.

- [***yfinance:***](https://github.com/ranaroussi/yfinance) Python library for retrieving Yahoo Finance data.

- [***pandas:***](https://pandas.pydata.org/) Library for data manipulation and analysis.

- [***numpy:***](https://numpy.org/) Library for numerical computations.

- [***scikit-learn:***](https://scikit-learn.org/) Machine learning library used for building the models and evaluating performance.



