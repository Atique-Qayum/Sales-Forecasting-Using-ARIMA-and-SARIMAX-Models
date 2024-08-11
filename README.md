[View The Project Details (PDF)](https://github.com/Atique-Qayum/project_ARIMA/blob/main/ARIMA_project/ISP%20Report%20PGD%20DSAI%20Final%20(Muhammad%20Atique%20Qayum)%20.pdf)

# Sales Forecasting Using ARIMA and SARIMAX Models

## Table of Contents

- [List of Abbreviations and Symbols](#list-of-abbreviations-and-symbols)
- [Acknowledgment](#acknowledgment)
- [Abstract](#abstract)
- [Introduction](#introduction)
  - [Significance of the Topic](#significance-of-the-topic)
  - [Evolution](#evolution)
  - [Pros and Cons](#pros-and-cons)
  - [Why Forecasting](#why-forecasting)
  - [Challenging Aspects](#challenging-aspects)
  - [Scope and Objectives](#scope-and-objectives)
  - [Brief Methodology](#brief-methodology)
- [Background Study](#background-study)
  - [Literature Review](#literature-review)
    - [Overview: Sales Forecasting and Relevant Models](#overview-sales-forecasting-and-relevant-models)
    - [Sales Forecasting Techniques](#sales-forecasting-techniques)
    - [Time Series Analysis in Sales Forecasting](#time-series-analysis-in-sales-forecasting)
    - [ARIMA Model](#arima-model)
    - [SARIMAX Model](#sarimax-model)
    - [AUTO ARIMA Model](#auto-arima-model)
    - [Machine Learning in Sales Forecasting](#machine-learning-in-sales-forecasting)
    - [Stationarity](#stationarity)
    - [Differencing](#differencing)
    - [Determining the AR Term (p)](#determining-the-ar-term-p)
    - [Determining the MA Term (q)](#determining-the-ma-term-q)
    - [Statistical Tests Used](#statistical-tests-used)
    - [Model Evaluation Metrics](#model-evaluation-metrics)
    - [Seasonal Differencing](#seasonal-differencing)
    - [Exogenous Variables in SARIMAX](#exogenous-variables-in-sarimax)
    - [Detailed Review of Studies on ARIMA, AUTO ARIMA, and SARIMAX](#detailed-review-of-studies-on-arima-auto-arima-and-sarimax)
    - [Hybrid Models](#hybrid-models)
    - [Comparison of Forecasting Models](#comparison-of-forecasting-models)
    - [Case Studies in Sales Forecasting](#case-studies-in-sales-forecasting)
    - [Gap Analysis](#gap-analysis)
    - [Relevance to Current Project](#relevance-to-current-project)
    - [Summary](#summary)
- [Methodology](#methodology)
  - [Data Collection](#data-collection)
  - [Data Preprocessing](#data-preprocessing)
  - [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
  - [Model Development](#model-development)
  - [Model Evaluation](#model-evaluation)
  - [Conclusion](#conclusion)
- [The Main Body of the Report / Findings](#the-main-body-of-the-report--findings)
  - [Load and Preprocess the Data](#load-and-preprocess-the-data)
  - [Exploratory Data Analysis (EDA) Findings](#exploratory-data-analysis-eda-findings)
- [Conclusions and Recommendations](#conclusions-and-recommendations)
  - [Conclusions](#conclusions)
  - [Recommendations](#recommendations)
- [References](#references)


---

## List of Abbreviations and Symbols

- **ARIMA**: AutoRegressive Integrated Moving Average
- **SARIMAX**: Seasonal AutoRegressive Integrated Moving Average with eXogenous factors
- **AUTO ARIMA**: Automatic AutoRegressive Integrated Moving Average
- **EDA**: Exploratory Data Analysis
- **MAE**: Mean Absolute Error
- **MAPE**: Mean Absolute Percentage Error
- **MSE**: Mean Squared Error
- **RMSE**: Root Mean Squared Error
- **AIC**: Akaike Information Criterion
- **BIC**: Bayesian Information Criterion
- **PACF**: Partial AutoCorrelation Function
- **ACF**: AutoCorrelation Function
- **R**: A programming language and free software environment for statistical computing and graphics
- **Python**: A high-level programming language used for general-purpose programming
- **p**: Number of lag observations included in the model (for AR terms)
- **d**: Number of times that the raw observations are differenced
- **q**: Size of the moving average window
- **P**: Seasonal autoregressive order
- **D**: Seasonal differencing order
- **Q**: Seasonal moving average order
- **m**: Number of periods in each season
- **y(t)**: Value of the time series at time t
- **E**: Expected value operator

*These abbreviations and symbols are used throughout the report to denote specific models, statistical terms, and key metrics related to the analysis and forecasting of sales data.*

---

## Acknowledgment

First praise is to Allah, the Almighty, on whom ultimately we depend for sustenance and guidance.

Acknowledgment is due to NED University of Engineering & Technology, Karachi for the support it has provided me for the completion of the project. I would like to thank Dr. Najeed Ahmed, the project supervisor for proposing this advanced topic for the project and for meaningful advice at each step, he helped me remain on track and provided necessary guidance for the project and report completion.

In addition, I would also like to express my gratitude to my loving and considerate family, who graciously allowed me the precious time I needed, despite the domestic chores I was spared for. Special thanks to my batch fellows, who remained a source of encouragement for me by way of their valuable comments & suggestions.

---

## Abstract

This report offers an in-depth analysis and predictive modeling approach for forecasting future sales using ARIMA and SARIMAX models. The study aims to understand sales trends, customer behavior, and product performance to deliver actionable insights for business decision-making. The methodology encompasses data collection, preprocessing, exploratory data analysis (EDA), and the development of ARIMA, SARIMAX, and AUTO ARIMA models.

Key findings from the EDA reveal significant seasonal peaks, top-performing products, and regional sales variations. The SARIMAX model demonstrated superior performance by effectively capturing seasonality and external factors. The report underscores the importance of customer retention and high-value customers.

The study concludes that accurate sales forecasts can enhance inventory management, targeted marketing, and customer retention strategies. Future recommendations include incorporating additional data sources, exploring advanced machine learning models, and implementing real-time data analysis systems. The report aims to provide valuable insights and practical recommendations to drive business growth and improve overall performance.

---

## Introduction

### Significance of the Topic

Sales forecasting is essential for effective business strategy and operational planning. It allows companies to make well-informed decisions regarding inventory, staffing, budgeting, and marketing. In today's competitive landscape, the ability to predict future sales trends offers a substantial edge. For example, by understanding seasonal variations, peak sales periods, and new market trends, businesses can optimize their operations and increase profitability. Additionally, sales forecasting supports risk management by helping businesses prepare for potential downturns or unexpected market changes.

Accurate sales forecasts lead to better inventory management, higher customer satisfaction, and improved financial planning. Conversely, inaccurate forecasts can cause overstocking, stockouts, and missed opportunities.

![fig01.](https://github.com/Atique-Qayum/project_ARIMA/blob/main/ARIMA_project/importance_of_forecasting.png)

### Evolution

Sales forecasting has undergone significant advancements over the years. Initially, businesses used basic methods like moving averages and expert judgment to predict sales, but these approaches often lacked the precision needed to handle complex market dynamics.

The mid-20th century saw the advent of computers and data analytics, leading to the development of more advanced statistical methods. The 1970s introduced time series analysis techniques such as ARIMA (AutoRegressive Integrated Moving Average), which significantly improved sales forecasting by systematically modeling time series data and accurately capturing trends, seasonality, and cyclic patterns.

In recent years, machine learning and artificial intelligence (AI) have further transformed sales forecasting. Techniques like SARIMAX (Seasonal AutoRegressive Integrated Moving Average with eXogenous factors) and AUTO ARIMA automate model selection and integrate external variables, greatly enhancing forecast accuracy and reliability. These innovations have elevated sales forecasting from a basic process to a sophisticated, data-driven practice.

### Pros and Cons

**Pros:**

- **Informed Decision-Making:** Accurate forecasts offer valuable insights for strategic planning and operational decisions.
- **Resource Optimization:** Businesses can efficiently manage inventory, workforce, and finances, minimizing waste and boosting efficiency.
- **Risk Management:** Forecasting enables anticipation of market shifts and preparation for potential risks, improving business resilience.
- **Competitive Advantage:** Accurate sales forecasting allows businesses to stay ahead of competitors by identifying trends and opportunities early.

**Cons:**

- **Data Dependency:** The reliability of sales forecasts is highly dependent on the quality and completeness of historical data.
- **Complexity:** Implementing advanced forecasting models can be complex and requires specialized knowledge and skills.
- **Uncertainty:** Despite using sophisticated models, forecasts are inherently uncertain and can be influenced by unforeseen events or market changes.
- **Cost:** Developing and maintaining advanced forecasting systems can be expensive, especially for small businesses.

### Why Forecasting

Sales forecasting is crucial for various reasons.

Firstly, it acts as a roadmap, helping businesses set realistic goals and expectations. By predicting future sales, companies can create strategies that align with market demand, ensuring they meet customer needs while avoiding overproduction or stockouts.

Secondly, it aids in financial planning and budgeting. Accurate forecasts allow businesses to allocate resources efficiently, plan investments, and manage cash flow effectively. This is particularly important for businesses with limited resources, where financial errors can have significant impacts.

Thirdly, forecasting enhances customer satisfaction by ensuring product availability and timely delivery. By understanding sales patterns, businesses can maintain optimal inventory levels, reducing the risk of stockouts or excess inventory. This not only improves customer experience but also minimizes carrying costs and potential losses from unsold goods.

Lastly, sales forecasting is vital for strategic planning and market competitiveness. Companies that accurately predict market trends and consumer behavior are better positioned to seize opportunities and mitigate risks. This proactive approach helps them stay ahead of competitors and adapt swiftly to changing market conditions. The increasing complexity of business environments and the availability of large datasets underscore the need for accurate sales forecasting. Effective forecasting enables better planning and execution, providing a competitive edge by allowing companies to anticipate demand, optimize resources, and respond proactively to market changes.

### Challenging Aspects

Despite its advantages, sales forecasting comes with several challenges.

One major challenge is the quality and availability of data. Accurate forecasts depend on historical sales data, which may be incomplete or unreliable. Issues like missing data, inconsistencies, and errors can significantly affect forecast accuracy.

Another challenge is the complexity of forecasting models. Advanced models such as ARIMA and SARIMAX require a deep understanding of statistical methods and time series analysis. Implementing these models can be resource-intensive, necessitating specialized skills and knowledge that may not be readily available within an organization.
![fig02.](https://github.com/Atique-Qayum/project_ARIMA/blob/main/ARIMA_project/challenges.png)

Additionally, the dynamic nature of markets poses a challenge to forecasting. Economic conditions, consumer preferences, and competitive actions can change rapidly, making it difficult to predict future sales accurately. External factors like political events, natural disasters, or technological advancements can further complicate forecasting efforts.

Finally, forecasting always involves some level of uncertainty. Even the most sophisticated models cannot predict the future with complete certainty. Businesses must be prepared to manage this uncertainty and adjust their strategies as new information becomes available.

### Scope and Objectives

The main goal of this study is to evaluate and compare various time series forecasting models, including ARIMA, SARIMAX, and AUTO ARIMA, to assess their effectiveness in predicting sales data. The study aims to identify the most accurate model and offer insights for enhancing future sales forecasting.

**Scope of this project includes:**

- **Data Collection and Preprocessing:** Gathering and preparing historical sales data to ensure it is suitable for analysis.
- **Exploratory Data Analysis (EDA):** Examining the data to reveal patterns, trends, and insights that guide model development.
- **Model Development:** Creating and assessing ARIMA, SARIMAX, and AUTO ARIMA models for forecasting future sales.
- **Model Comparison:** Evaluating the performance of each model to determine the most accurate and reliable one.
- **Interpretation and Recommendations:** Providing actionable insights and suggestions based on the forecasted data.

**Primary objectives of this project are:**

- To analyze historical sales patterns and identify significant trends.
- To develop precise forecasting models that predict future sales effectively.
- To compare the performance of different models and select the most effective one.
- To offer practical recommendations for business strategy based on the sales forecasts.

### Brief Methodology

The methodology for this project follows several key steps:

1. **Data Collection:** The dataset spans from 2016 to 2018 and includes information on orders, customers, and sales amounts.

2. **Data Preprocessing:** This phase involves cleaning the data by addressing missing values, removing duplicates, and ensuring consistency. Techniques such as interpolation and forward/backward filling are applied to manage incomplete data.

3. **Exploratory Data Analysis (EDA):** EDA is performed to visualize and summarize the data, revealing patterns and insights. This includes analyzing sales trends on a monthly and yearly basis, identifying top-performing products and cities, and understanding customer behavior.

4. **Model Development:**
   - **ARIMA:** This model is designed to capture the autoregressive and moving average components of the sales data.
   - **SARIMAX:** This model accounts for seasonal effects and external variables, offering a more detailed forecast.
   - **AUTO ARIMA:** AUTO ARIMA automates the model selection process, determining the optimal parameters for the ARIMA model.

5. **Model Evaluation:** The models are assessed using metrics such as RMSE (Root Mean Squared Error) and MAE (Mean Absolute Error) to gauge their accuracy and reliability.

6. **Interpretation and Recommendations:** The forecasted data is analyzed to provide actionable insights and recommendations for business strategy, including optimizing inventory, planning marketing efforts, and making informed financial decisions.

This methodical approach ensures a thorough analysis of sales data, resulting in accurate forecasts and practical business recommendations.

---

## Background Study

### Literature Review

#### Overview: Sales Forecasting and Relevant Models

Sales forecasting is a vital focus in business analytics and operations management. Precise forecasting allows businesses to make well-informed decisions regarding inventory management, financial planning, and strategic initiatives. Over time, a range of models and techniques has been developed to predict sales, evolving from basic statistical methods to advanced machine learning algorithms.

#### Sales Forecasting Techniques

Sales forecasting techniques can be divided into two main categories: qualitative and quantitative methods. Qualitative methods depend on expert judgment and intuition, making them effective for short-term forecasts or when historical data is scarce. In contrast, quantitative methods use historical data and mathematical models to predict future sales, making them more suitable for long-term forecasting when there is ample historical data.

Forecasting models can also be classified into traditional statistical approaches and modern machine learning techniques. Traditional methods, like ARIMA, aim to identify patterns in historical data, while machine learning techniques are capable of managing more complex relationships and larger datasets.

#### Time Series Analysis in Sales Forecasting

Time series analysis is a valuable technique for forecasting sales. It entails examining a sequence of data points recorded at consistent time intervals to detect patterns and trends. Time series models, like ARIMA (AutoRegressive Integrated Moving Average), are commonly employed in forecasting due to their ability to identify underlying patterns in the data, such as trends and seasonal variations.

Machine learning has transformed time series forecasting by facilitating the analysis of large datasets and intricate patterns. Techniques including neural networks, support vector machines, and ensemble methods have demonstrated potential in enhancing forecast accuracy.

#### ARIMA Model

The ARIMA model, developed by Box and Jenkins in the 1970s, is a widely used tool for time series forecasting. It integrates autoregressive (AR) and moving average (MA) components with differencing to stabilize the time series data. ARIMA is particularly effective for short-term forecasts and can accommodate various types of time series data.

In the ARIMA model:

- **p** denotes the number of lagged observations (autoregressive terms),
- **d** represents the number of differencing operations needed to achieve stationarity,
- **q** indicates the size of the moving average window (moving average terms).
![fig03.](https://github.com/Atique-Qayum/project_ARIMA/blob/main/ARIMA_project/ARIMA.png)


These parameters are selected based on the data's characteristics and are often determined using ACF (Autocorrelation Function) and PACF (Partial Autocorrelation Function) plots.

ARIMA (AutoRegressive Integrated Moving Average) is renowned for its effectiveness in capturing linear patterns in time series data. However, it may encounter difficulties with non-linear relationships and seasonal variations. The AR component involves regressing the variable on its previous values, the I component handles differencing to ensure stationarity, and the MA component models the error term as a linear combination of previous error terms.

ARIMA is versatile in modeling both short-term and long-term dependencies and is suitable for a broad range of applications. It can be extended to address seasonality through SARIMA (Seasonal ARIMA). Additionally, parameter optimization can be streamlined using AUTO ARIMA, which automates the selection of the most suitable model.

#### SARIMAX Model

The SARIMAX (Seasonal AutoRegressive Integrated Moving Average with eXogenous factors) model enhances the ARIMA framework by incorporating seasonal elements and external variables. This extension makes SARIMAX ideal for data exhibiting seasonal patterns and influenced by external factors, such as marketing activities or economic indicators. It is commonly used in sectors where seasonality is a significant factor, such as retail and tourism.
![fig04.](https://github.com/Atique-Qayum/project_ARIMA/blob/main/ARIMA_project/SARIMAX.png)

Similarly, the SARIMA (Seasonal AutoRegressive Integrated Moving Average) model builds upon ARIMA to address seasonal variations in data. It introduces additional seasonal parameters—P, D, Q, and S—to capture seasonal patterns. These parameters represent the autoregressive terms (P), differencing (D), and moving average terms (Q) for the seasonal component, with S denoting the length of the seasonal cycle. SARIMA is particularly effective for datasets with pronounced seasonal effects, such as monthly sales data with annual seasonality.

#### AUTO ARIMA Model

AUTO ARIMA streamlines the process of selecting the optimal parameters for the ARIMA model by automating it. It employs algorithms to explore various combinations of the p, d, and q parameters—representing the autoregressive order, differencing order, and moving average order, respectively. This automation not only simplifies the model selection process but often leads to more precise forecasts.

The approach involves testing different parameter combinations (p, d, q) and choosing the model that minimizes a specific criterion, such as the AIC (Akaike Information Criterion) or BIC (Bayesian Information Criterion). AUTO ARIMA eliminates the need for manual adjustments and is especially beneficial for large datasets or complex time series. This method reduces manual tuning requirements and has been proven to enhance forecast accuracy across various applications.

#### Machine Learning in Sales Forecasting

Machine learning methods have become increasingly popular in sales forecasting because they can manage large datasets and identify complex patterns. Algorithms like decision trees, random forests, and neural networks excel at uncovering non-linear relationships and interactions between variables. These models are especially valuable when traditional time series approaches struggle to address the data's complexity.
![fig05.](https://github.com/Atique-Qayum/project_ARIMA/blob/main/ARIMA_project/ML%20is%20Sales.png)

#### Stationarity

A stationary time series is characterized by statistical properties such as mean and variance that remain constant over time. Stationarity is essential for time series modeling, as many forecasting methods, including ARIMA, assume that the data is stationary. To achieve stationarity, techniques such as differencing, transformation, or detrending are employed.

#### Differencing

Differencing in time series involves calculating the difference between consecutive observations to make a time series stationary by removing trends and seasonality. This technique helps stabilize the mean of the series, facilitating easier modeling with methods such as ARIMA.

**Determining the Value of d:**

- If the series is non-stationary, the first difference is computed to check if it results in a stationary series.
- Using a single lag is preferred due to its simplicity, lower risk of overfitting, and evidence of stationarity, as shown by an extreme test statistic and a very low p-value.

**Advantages of Using One Lag:**

1. **Simplicity:** Fewer parameters create a more straightforward and interpretable model.
2. **Data Preservation:** Minimal loss of data, which is important for smaller datasets.
3. **Reduced Overfitting Risk:** Lower risk of overfitting improves model generalizability.
4. **Efficiency:** Lower computational cost and faster model fitting.
5. **Sufficient Stationarity:** Strong evidence of stationarity indicated by extreme test statistics and very low p-values.
6. **Easier Diagnostics:** Simplified residual analysis and model diagnostics.

#### Determining the AR Term (p)

The AR term in the ARIMA model denotes the number of lagged observations incorporated into the model. The appropriate order for the AR term is identified using the Partial Autocorrelation Function (PACF) plot, which shows the direct correlation between a lag and the series. The AR term's order corresponds to the number of lags that exceed the significance threshold on the PACF plot.

**Partial Autocorrelation Function (PACF):**

- The PACF illustrates the direct correlation between a lag and the series.
- The order of the AR term is determined by the number of lags that surpass the significance limit on the PACF plot.

#### Determining the MA Term (q)

The MA term in the ARIMA model signifies the size of the moving average window. Its value is determined using the Autocorrelation Function (ACF) plot, which helps ascertain the number of MA terms needed to eliminate autocorrelation in the stationary series. An MA term represents the error in the lagged forecast, and the ACF plot visually depicts the autocorrelation structure of the series.

**Autocorrelation Function (ACF):**

- The MA term reflects the error associated with the lagged forecast.
- The ACF plot determines how many MA terms are necessary to address autocorrelation in the stationary series.

#### Statistical Tests Used

Various statistical tests are employed to validate the assumptions of time series models, including:

- **Augmented Dickey-Fuller (ADF) Test:** Assesses whether the time series is stationary.
- **Ljung-Box Test:** Evaluates whether there is any serial correlation in the residuals.
- **Durbin-Watson Test:** Detects the presence of autocorrelation in the residuals.

#### Model Evaluation Metrics

Assessing the performance of time series models is essential for verifying their accuracy and reliability. Key evaluation metrics for ARIMA and SARIMA models include:

- **Mean Absolute Error (MAE):** Measures the average absolute difference between observed and predicted values.
- **Root Mean Squared Error (RMSE):** Represents the square root of the average squared difference between observed and predicted values.
- **Mean Absolute Percentage Error (MAPE):** Calculates the average absolute percentage difference between observed and predicted values.
- **AIC/BIC:** Model selection criteria that penalize the number of parameters to avoid overfitting.

These metrics offer quantitative insights into a model's accuracy and facilitate the comparison of different models' performance.

#### Seasonal Differencing

Seasonal differencing entails subtracting the value of an observation from the same period in the previous cycle. For example, with monthly data, this would involve subtracting the value from the same month in the previous year. This method helps eliminate seasonal patterns and stabilize variance.

#### Exogenous Variables in SARIMAX

Exogenous variables are external factors that can impact the time series. In SARIMAX models, incorporating these variables enhances the model’s predictive accuracy. Examples of exogenous variables include economic indicators, marketing expenditures, or other relevant factors that influence sales.

#### Detailed Review of Studies on ARIMA, AUTO ARIMA, and SARIMAX

1. **ARIMA Models:**
   - The foundation for ARIMA modeling was established by Box and Jenkins (1970) through their structured approach.
   - Recent research has aimed at enhancing ARIMA models by integrating machine learning techniques to boost accuracy.

2. **AUTO ARIMA:**
   - The concept of AUTO ARIMA was introduced by Hyndman and Khandakar (2008), automating the model selection process and significantly reducing the need for manual intervention and expertise.
   - Research has demonstrated that AUTO ARIMA often outperforms manually configured ARIMA models, particularly with complex datasets.

3. **SARIMAX Models:**
   - Recent studies have underscored SARIMAX's effectiveness in accounting for seasonality and external variables.
   - Its application across various sectors, including retail and finance, has shown its effectiveness in enhancing forecast accuracy.

#### Hybrid Models

Hybrid models leverage the strengths of multiple forecasting techniques to enhance accuracy. For instance, a hybrid approach might integrate ARIMA with a neural network to capture both linear and non-linear patterns in the data. Research indicates that hybrid models frequently surpass the performance of individual models, especially in complex forecasting situations.

#### Comparison of Forecasting Models

Various studies have evaluated and compared the performance of different forecasting models. For example, Makridakis et al. (2018) performed an extensive comparison of 104 forecasting methods, encompassing both statistical and machine learning approaches. The study revealed that no single model consistently excelled across all datasets, underscoring the need for careful model selection and customization based on the specific context and characteristics of the data.

#### Case Studies in Sales Forecasting

Case studies offer valuable insights into the practical application of forecasting models in real-world situations. For instance, one case study might illustrate how SARIMAX was employed to forecast sales during holiday seasons for a retail chain, while another might showcase the use of machine learning models to predict sales for a new product launch. These case studies reveal the practical challenges and advantages associated with various forecasting techniques.

#### Gap Analysis

Despite significant progress in sales forecasting, several gaps and limitations persist. One major issue is dealing with external factors and sudden market shifts. Traditional time series models often assume that historical trends will continue, which may not be accurate in rapidly changing markets. Another challenge is the requirement for extensive historical data, which may not be available for new products or emerging markets. Additionally, the complexity and resource demands of advanced models can be prohibitive for smaller businesses.

Although ARIMA and SARIMA models have been extensively studied and used, they still have limitations. A key drawback is their dependence on historical data, which may not always be reliable or available. These traditional models can also struggle with capturing complex non-linear patterns in the data. While recent advancements in machine learning and deep learning offer promising alternatives, further research is needed to assess their performance compared to traditional models.

Another area needing attention is the integration of external factors (exogenous variables) into ARIMA and SARIMA models. While SARIMAX models address this issue, more research is required to understand how different exogenous variables impact forecasting accuracy. Additionally, there is a need for more domain-specific research on the application of ARIMA and SARIMA models in industries such as retail and finance to better understand their effectiveness and limitations.

#### Relevance to Current Project

This project is designed to address several gaps identified in current research. By integrating external variables and utilizing AUTO ARIMA to automate the model selection process, the project aims to enhance the accuracy and reliability of sales forecasts. Furthermore, by evaluating the performance of various models, the project will offer insights into the most effective forecasting techniques for different types of sales data.

#### Summary

In summary, this literature review outlines the fundamental concepts and methods related to time series analysis and sales forecasting. It covers the importance of sales forecasting, the development of time series models, and the strengths and weaknesses of ARIMA and SARIMA models. The review also addresses key aspects such as model parameters, stationarity, differencing, and evaluation metrics. Additionally, it explores recent advancements, including AUTO ARIMA and the incorporation of external variables in SARIMAX models.

The identified gaps in current research highlight the need for further exploration of advanced machine learning techniques and the integration of external factors in time series forecasting. This project aims to bridge these gaps by developing and comparing ARIMA, SARIMAX, and AUTO ARIMA models for sales forecasting. The outcomes of this project will enhance the existing knowledge base and offer practical recommendations for businesses seeking to refine their sales forecasting methods.

The literature on sales forecasting spans various approaches, from traditional time series models to sophisticated machine learning algorithms. While ARIMA and SARIMAX models are valued for their capability to identify trends and seasonal patterns, machine learning models provide greater flexibility and can manage complex data patterns. Despite these advancements, challenges persist regarding the handling of external factors, unexpected market shifts, and data constraints. This project extends current research by integrating external variables, automating model selection, and comparing different forecasting techniques to deliver actionable insights for businesses.

---
# Methodology

## Data Collection

The dataset for this study was obtained from a retail company's sales records spanning the last five years. It includes:
- **Monthly Sales Data**
- **Product Categories**
- **Sales Regions**

## Data Preprocessing

To ensure the dataset is suitable for analysis, several preprocessing steps were performed:

1. **Handling Missing Values:**
   - Imputed numerical values (e.g., Quantity Sold, Sales Amount) using mean or median.
   - Filled missing categorical attributes (e.g., Product Category, Customer Location) using the most common category or predictive techniques.

2. **Removing Duplicates:**
   - Identified and eliminated duplicate records to avoid double counting and ensure accurate analysis.

3. **Data Type Conversion:**
   - Reformatted Order Date to a date-time format.
   - Adjusted numerical attributes to appropriate integer or float types.

4. **Outlier Detection and Treatment:**
   - Identified outliers using Z-score and Interquartile Range (IQR).
   - Corrected or removed erroneous outliers.

5. **Creating Additional Features:**
   - Generated new features like Month-Year from Order Date for monthly sales analysis.
   - Introduced Day of Week feature to examine sales patterns by day.

## Exploratory Data Analysis (EDA)

EDA was conducted to identify patterns, trends, and insights within the data using the following methods:

1. **Descriptive Statistics:**
   - Summarized key attributes using mean, median, standard deviation, and range.

2. **Visualization Techniques:**
   - **Line Charts:** Illustrated sales trends over time.
   - **Bar Charts:** Highlighted top-selling products and categories.
   - **Heatmaps:** Analyzed sales patterns across geographic locations.
   - **Box Plots:** Identified outliers and examined sales amount distribution.

3. **Correlation Analysis:**
   - Examined relationships between attributes using correlation matrices and scatter plots.

4. **Seasonal Decomposition:**
   - Decomposed time series data into trend, seasonal, and residual components to reveal underlying patterns.

## Model Development

Three different forecasting models were developed and evaluated: ARIMA, SARIMAX, and AUTO ARIMA.

### ARIMA Model

**ARIMA (AutoRegressive Integrated Moving Average)**

1. **Model Identification:**
   - Determined the order of the ARIMA model (p, d, q) using Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots.

2. **Parameter Estimation:**
   - Estimated parameters using Maximum Likelihood Estimation (MLE) to minimize error.

3. **Model Diagnostics:**
   - Conducted diagnostic checks to ensure the residuals resembled white noise.

4. **Forecasting:**
   - Used the ARIMA model to generate and plot future sales forecasts.

### SARIMAX Model

**SARIMAX (Seasonal AutoRegressive Integrated Moving Average with eXogenous factors)**

1. **Seasonal Component Identification:**
   - Identified seasonal components and determined seasonal order (P, D, Q) using seasonal decomposition and ACF/PACF plots.

2. **External Variables:**
   - Incorporated relevant external variables (e.g., marketing expenditures, economic indicators) into the model.

3. **Model Estimation:**
   - Estimated the SARIMAX model using MLE to optimize parameters.

4. **Model Diagnostics:**
   - Conducted diagnostic checks to confirm residuals resembled white noise.

5. **Forecasting:**
   - Utilized the SARIMAX model to produce and compare forecasts against actual sales data.

### AUTO ARIMA Model

**AUTO ARIMA**

1. **Parameter Search:**
   - Employed algorithms to find the best combination of (p, d, q) parameters using Akaike Information Criterion (AIC) or Bayesian Information Criterion (BIC).

2. **Model Fitting:**
   - Fitted the chosen model to historical sales data using MLE.

3. **Model Diagnostics:**
   - Conducted diagnostic checks to confirm residuals resembled white noise.

4. **Forecasting:**
   - Used the AUTO ARIMA model to generate and assess sales forecasts.

## Model Evaluation

The performance of the forecasting models was assessed using the following metrics:

1. **Root Mean Squared Error (RMSE):** 
   - Calculates the square root of the average squared differences between forecasted and actual values.

2. **Mean Absolute Error (MAE):** 
   - Measures the average absolute differences between forecasted and actual values.

3. **Mean Absolute Percentage Error (MAPE):**
   - Calculates the average absolute percentage differences between forecasted and actual values.

4. **R-squared (R²):**
   - Quantifies the proportion of variance in actual values explained by the forecasted values.

## Conclusion

This methodology outlines a comprehensive approach to sales forecasting using advanced time series models. By employing ARIMA, SARIMAX, and AUTO ARIMA models, the goal is to produce accurate sales forecasts that support strategic decision-making and improve business performance. Systematic data preprocessing, thorough EDA, and rigorous model evaluation ensure the reliability and robustness of the forecasting models, ultimately aiding in the business's success.



# The Main Body of the Report / Findings

## 1. Load and Preprocess the Data
The sales data covers a period of three years (2016-2018). The preprocessing steps involve:
- **Cleaning the Data**: Handling missing values, correcting data types, and eliminating duplicates.
- **Key Findings**:
  - 2016: 4,741 orders, $899,534.63 in sales
  - 2017: 572,505 orders, $82,060,567.36 in sales
  - 2018: 471,329 orders, $66,826,463.61 in sales

## 2. Exploratory Data Analysis (EDA) Findings

### Yearly Sales Report
An analysis of yearly sales data reveals the following trends:
- **2016**: Significant growth in sales and orders.
- **2017**: Peak year with the highest sales and orders.
- **2018**: A slight decline in sales compared to 2017.

### Top 5 Products Sold by Quantity Each Year
- **2016**: Top product sold 672 units.
- **2017**: Top product sold 15,595 units.
- **2018**: Top product sold 13,454 units.

### Top 5 Products by Total Sales Each Year
- **2016**: Highest sales for a product was $255,346.56.
- **2017**: Highest sales for a product was $3,207,794.00.
- **2018**: Highest sales for a product was $1,674,118.49.

### Top 5 Cities by Sales Each Year
- **2016**: Santos leads with $255,346.56 in sales.
- **2017**: Rio de Janeiro leads with $8,540,428.36 in sales.
- **2018**: Rio de Janeiro leads again with $7,420,526.64 in sales.

### Top 5 Sellers by Sales Each Year
- **2016**: Top seller achieved $255,346.56 in sales.
- **2017**: Top seller achieved $11,968,497.99 in sales.
- **2018**: Top seller achieved $6,460,352.20 in sales.

### Sales Data by Payment Type Each Year
- **2016**: Credit Card was the most popular payment method with $453,334.33 in sales.
- **2017**: Credit Card led with $33,825,730.20 in sales.
- **2018**: Credit Card again led with $32,885,941.40 in sales.

### Monthly and Yearly Sales Trends
- **Monthly Trends**: Sales peaks during festive seasons, especially in November and December.
- **Yearly Trends**: Rapid growth from 2016 to 2017, followed by a slight decline in 2018.

## 3. Time Series Analysis and Forecasting

### Data Preprocessing for Time Series
- **Aggregation**: Sales data is aggregated into daily totals for trend and pattern analysis.

### Perform Stationary Tests
- **ADF Test**: ADF test confirmed the data is stationary after differencing.

### Differencing
- **Seasonal Differencing**: Applied to remove seasonal trends.

### Generate Correlograms (ACF & PACF)
- **Correlograms**: ACF and PACF plots help determine appropriate lags for AR and MA components.

### Apply Different ARIMA Models

#### ARIMA Model (ARIMA(1, 1, 1))
- **Key Insights**: Issues with non-normality and heteroskedasticity in the residuals.

#### SARIMAX Model (SARIMAX(1, 1, 2)x(1, 1, 2, 30))
- **Key Insights**: Lower AIC and BIC but issues with non-significant terms and residuals.

#### Auto ARIMA 
- **Model**: SARIMAX(2, 1, 0)x(2, 1, 0, 12)
- **Key Insights**: Significant terms but issues with residual autocorrelation and non-normality.

### Auto ARIMA Forecast for the Last 15 Days
- **Model**: SARIMAX(1, 1, 2)
- **Forecast Evaluation**: Compared forecasts with actual sales to assess model performance.

### Plot and Evaluate the Results
- **Visual Assessment**: Plots of actual vs. forecasted sales.
- **Evaluation Metrics**: Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE) used to assess accuracy.

## Conclusion
The analysis reveals key insights into sales trends, top-performing products, cities, sellers, and consumer payment preferences. The time series forecasting models provide valuable predictions, though with some limitations related to residuals and seasonality.


# Conclusions and Recommendations

## Conclusions

#### Summary of Key Findings
The analysis of sales data from 2016 to 2018 reveals several key trends and patterns:
- **Order Quantity and Total Sales:** There was a significant rise in both order quantity and total sales in 2017, followed by a decline in 2018.
- **Product and Seller Performance:** Certain products and sellers consistently performed well, but the top performers varied considerably from year to year.
- **Geographical Insights:** Rio de Janeiro stood out as a major sales hub, especially in 2017 and 2018, despite experiencing a slight decrease in sales in 2018.
- **Sales Surge in 2017:** The dramatic increase in sales for top-selling products and sellers in 2017 suggests the influence of external factors or effective marketing strategies during that year.

#### EDA Findings
- **Sales Trends:** The data reveals seasonal peaks and notable yearly growth, underscoring the impact of festive seasons on sales.
- **Market Insights:** Top products, cities, and sellers offer valuable insights into market dynamics and consumer preferences.

#### Model Performance
- Among the ARIMA, SARIMAX, and AUTO ARIMA models, SARIMAX demonstrated the best performance based on AIC and BIC criteria. Despite this, all models showed issues with non-normality and heteroskedasticity in the residuals. Specifically, the SARIMAX(1, 1, 2) model provided the most accurate daily sales forecasts, effectively capturing seasonal patterns and key sales influencers. However, residual diagnostics indicated non-normality and heteroskedasticity, which need to be addressed.
- **Forecast Accuracy:** The forecasts for the last 15 days were reasonably accurate, with low MAE and RMSE values.

### Impacts
Accurate sales forecasting enhances inventory management by minimizing the risk of stockouts and overstocking. It also supports financial planning, allowing for optimal budget allocation and resource utilization.

### Future Work
Future research should investigate the integration of more advanced machine learning models, such as LSTM networks, to capture complex temporal dependencies. Including additional external factors, such as weather conditions and social media trends, could further improve forecast accuracy.

#### Advanced Techniques
- Explore deep learning models and hybrid approaches that combine ARIMA with neural networks.
- Incorporate more detailed external variables to enhance model performance.

#### Cross-Validation
- Apply cross-validation techniques to assess model performance on out-of-sample data.

#### Alternative Models
- Examine other time series models like Prophet or various machine learning approaches for better forecasts.
- Consider external influences, such as economic indicators and marketing campaigns, that might affect sales.

### Forecast Results
- **Forecast for 10 Days from the Last Data Point:**
  1. Day 1: $204,249.60
  2. Day 2: $204,482.94
  3. Day 3: $204,613.89
  4. Day 4: $204,676.55
  5. Day 5: $204,707.69
  6. Day 6: $204,722.58
  7. Day 7: $204,730.51
  8. Day 8: $204,734.75
  9. Day 9: $204,736.84
  10. Day 10: $204,737.87

### Model Performance Metrics
- **MAE (Mean Absolute Error):** $7.24
- **MSE (Mean Squared Error):** $100.35
- **RMSE (Root Mean Squared Error):** $10.02

### Conclusion
The analysis offers a detailed overview of sales trends, top products, key cities, and leading sellers from 2016 to 2018. The SARIMAX model successfully captures daily sales patterns, providing precise short-term forecasts. These insights can inform strategic decisions to enhance sales performance and improve inventory management.

## Recommendations

#### Actionable Recommendations
Based on the analysis, we recommend the following:
- **Model Selection:** Use the SARIMAX(1, 1, 2) model for daily sales forecasting due to its superior fit and significant coefficients.
- **Data Quality:** Conduct continuous data quality checks and preprocessing to ensure accuracy.
- **Model Updating:** Regularly update the model with new data to adapt to changing patterns.
- **Inventory Management:** Adjust inventory levels based on forecasted sales to reduce holding costs and avoid stockouts, focusing on consistently top-performing products.
- **Marketing Strategy:** Direct marketing efforts towards top-performing products and key cities like Rio de Janeiro and São Paulo for targeted campaigns and resource allocation to maximize sales.
- **Payment Methods:** Promote the use of credit cards and vouchers, as these are the most preferred payment methods.
- **Seasonal Promotions:** Utilize identified seasonal trends to plan targeted promotions and marketing campaigns during peak sales periods.
- **Customer Retention:** Implement loyalty programs and personalized marketing strategies to retain repeat customers and encourage frequent purchases.
- **Geographic Targeting:** Concentrate marketing efforts on top-performing cities to further boost sales in these key markets.
- **Continuous Monitoring:** Regularly update and monitor the forecasting models to incorporate new data and maintain prediction accuracy.

### Lessons Learned
The study highlights the critical role of data preprocessing, model selection, and diagnostic assessments in ensuring model reliability. It emphasizes the need to address issues such as non-normality and heteroskedasticity in residuals to enhance model performance.

- **Data Preprocessing:** Thorough data preprocessing is essential for accurate model results.
- **Model Diagnostics:** Regular diagnostic checks are vital for detecting and correcting problems with residuals.
- **Seasonal Components:** Incorporating seasonal components into the model significantly boosts accuracy.

### Technical Advantages
The SARIMAX model's capability to address seasonal patterns and include external variables offers a strong framework for forecasting sales. Meanwhile, AUTO ARIMA streamlines the model selection process, making it more accessible for businesses with limited statistical knowledge.

#### Model Improvement:
- **Model Refinement:** Test various model configurations and integrate external regressors.
- **Data Transformation:** Implement transformations to handle issues like heteroskedasticity and non-normality.
- **Cross-Validation:** Use out-of-sample data to assess model robustness and reliability.

### Limitations of the Study
- **Residual Issues:** Non-normality and heteroskedasticity in the residuals indicate a need for further model refinement.
- **Limited Data Duration:** The dataset spans only three years, which may not reflect long-term trends.
- **External Factors:** The current models do not account for external influences on sales.
- **Context-Specific Performance:** The effectiveness of the models may vary depending on the specific data context and characteristics.
- **Dependence on Historical Data:** The models are heavily reliant on historical data, which may not fully represent future market dynamics.
- **Data Quality:** The analysis is constrained by the data’s quality and detail. Enhanced data granularity could improve accuracy.
- **Potential for Improvement:** Future research could focus on advanced techniques, such as machine learning models, to enhance forecasting accuracy.
- **Incorporating External Factors:** Including variables like economic indicators or competitor activities could offer deeper insights into sales trends.
- **Diagnostic Concerns:** Issues such as non-normality and heteroskedasticity impact the reliability of the models.
- **Seasonal Patterns:** The current models may not fully capture all seasonal variations.

Addressing these limitations and implementing the suggested improvements can enhance sales forecasting and strategic planning, leading to better decision-making and increased profitability.

# References

1. Box, G. E. P., & Jenkins, G. M. (1970). Time Series Analysis: Forecasting and Control. Holden-Day.
2. Brockwell, P. J., & Davis, R. A. (2016). Introduction to Time Series and Forecasting (3rd ed.). Springer.
3. Brownlee, J. (2017). Introduction to Time Series Forecasting with Python. Machine Learning Mastery.
4. Chatfield, C. (2004). The Analysis of Time Series: An Introduction (6th ed.). Chapman and Hall/CRC.
5. Hyndman, R. J., & Athanasopoulos, G. (2018). Forecasting: Principles and Practice (2nd ed.). OTexts.
6. Makridakis, S., Wheelwright, S. C., & Hyndman, R. J. (1998). Forecasting: Methods and Applications (3rd ed.). John Wiley & Sons.
7. Montgomery, D. C., Jennings, C. L., & Kulahci, M. (2015). Introduction to Time Series Analysis and Forecasting. John Wiley & Sons.
8. Shumway, R. H., & Stoffer, D. S. (2017). Time Series Analysis and Its Applications: With R Examples (4th ed.). Springer.
9. Zhang, G. P. (2003). Time series forecasting using a hybrid ARIMA and neural network model. Neurocomputing, 50, 159-175.
10. Kumar, S. A., & Venkatesan, T. (2019). An Efficient Forecasting Model for Seasonal Time Series Data Using Hybrid ARIMA and SARIMA. International Journal of Computer Science and Network Security, 19(2), 44-51.
11. Williams, B. D., & Hoel, L. A. (2003). Modeling and Forecasting Vehicular Traffic Flow as a Seasonal ARIMA Process: Theoretical Basis and Empirical Results. Journal of Transportation Engineering, 129(6), 664-672.
12. Hyndman, R. J., & Khandakar, Y. (2008). Automatic Time Series Forecasting: The forecast Package for R. Journal
