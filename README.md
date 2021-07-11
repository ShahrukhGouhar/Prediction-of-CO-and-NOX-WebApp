# Prediction-of-CO-and-NOX Emission-WebApp
**OBJECTIVE**: Prediction of Gas Turbine CO and NOx Emission

**Description:** Predict the Gas Turbine CO and NOx Emission using 11 sensor measures aggregated over one hour (by means of average orsum) from a gas turbine located in Turkey's north western region for the purpose of studying flue gas emissions,namely CO and NOx (NO + NO2)

**Motivation:** Harmful effect of Flue gas emitted from power plant turbines on environment has always been a substantial concern. In the recent past years many peaceful protest to save environment has been seen. Environmental organization that seeks to protect, analyse or monitor the environment have conducted many events and activities to raise people awareness on environment. This project aims to predict emission of flue gases based on sensor data from gas turbine and various Machine Learning techniques.

The ML model can be used to predict/estimate amount of emission for future operations of Turbine and Turbine of same homologus series. Model output can also be used for validation and backing up of costly continuous emission monitoring systems used in gas-turbine-based power plants. Their implementation relies on the availability of appropriate and ecologically valid data.

**Data Source:** https://archive.ics.uci.edu/ml/datasets/Gas+Turbine+CO+and+NOx+Emission+Data+Set#

**Data Description:** The dataset contains 36733 instances of 11 sensor measures aggregated over one hour (by means of average or sum) from a gas turbine located in Turkey's north western region for the purpose of studying flue gas emissions, namely CO and NOx (NO + NO2).

**Variable (Abbr.) & Unit**

Ambient temperature (AT) C

Ambient pressure (AP) mbar

Ambient humidity (AH) (%)

Air filter difference pressure (AFDP) mbar

Gas turbine exhaust pressure (GTEP) mbar

Turbine inlet temperature (TIT) C

Turbine after temperature (TAT) C

Compressor discharge pressure (CDP) mbar

Turbine energy yield (TEY) MWH

Carbon monoxide (CO) mg/m^3

Nitrogen oxides (NOx) mg/m^3

**Tools Used:** Python, Jupyter-lab, Ms- Excel, Tableau

**Data Information**
**Attributes, their count and data type**

![image](https://user-images.githubusercontent.com/76644910/125195698-672cb900-e274-11eb-860d-bb83f9e763a7.png)

**First Five Rows of data**

![image](https://user-images.githubusercontent.com/76644910/125195723-875c7800-e274-11eb-9ce7-47d17979c897.png)

Attributes are on different scale. Like AT and AH are on the scale of 100 where has AP and TIT are on scale of 1000. So for ML models data set is scaled using standard scalar.

**Statistical Analysis**
**Statistical Summary of data**

![image](https://user-images.githubusercontent.com/76644910/125195745-a955fa80-e274-11eb-96f0-2c7bacffa4a6.png)

**Statistical Distribution of train data**

![image](https://user-images.githubusercontent.com/76644910/125195783-d3a7b800-e274-11eb-8ea6-9c6d999821ed.png)

**Correlation Analysis**

![image](https://user-images.githubusercontent.com/76644910/125195847-2e411400-e275-11eb-9f4e-9fda2625e03c.png)

**Variation of CO with other features**

![image](https://user-images.githubusercontent.com/76644910/125195883-59c3fe80-e275-11eb-9f66-927b4bc4507d.png)

**Variation of NOx with other features**

![image](https://user-images.githubusercontent.com/76644910/125195926-7f510800-e275-11eb-8197-db9c9aa5109a.png)

**Model Building**

First we split the data in train, cross validation and test set in the ratio of 60:20:20.
We built model on train set and tuned it on cross validation. Test data was kept aside for final evaluation.
Separate ML models were built for prediction of CO and NOx emission.
Using Forward addition and Backward Elimination method significant predictor variables were selected for CO and NOx prediction.

**Model Building Process of CO**

**Feature Engineering**
**Principle Component Analysis**
In statistical analysis using heat map we saw there was high multi – collinearity among the predictors.
So we applied PCA for removing multi – collinearity.  Below figure represent how predictors were combined after PCA. VO, V1, V2, V3 are principle components we found after PCA.

![image](https://user-images.githubusercontent.com/76644910/125195976-b45d5a80-e275-11eb-827d-7bb132498cf0.png)

V0, V1, V2 and V3 are principle components obtained after PCA.

Each row represents the coefficient of linear combination for respective principle component.

Linear Regressing Model built on above described PCA showed Adjusted_R^2 = 0.57 with MSE = 1.78 on cross validation set.

**Polynomial Feature Transformation**
Next we applied *Polynomial Feature transformation to get new features as a combination of old*
Below figure represent how features were combined after polynomial feature transformation

![image](https://user-images.githubusercontent.com/76644910/125196034-e4a4f900-e275-11eb-86bf-7ade9cab02c2.png)

Example for how variables have combined

V0 = (Old_VO^0) * (Old_V1^0) * (Old_V2^0) * (Old_V3^0)

V1 = (Old_VO^1) * (Old_V1^0) * (Old_V2^0) * (Old_V3^0)

V5 = (Old_VO^2) * (Old_V1^0) * (Old_V2^0) * (Old_V3^0)

V6 = (Old_VO^1) * (Old_V1^1) * (Old_V2^0) * (Old_V3^0) ...... & soon

Old_Vi’s are principle components and Vi’s are new set of features after feature transformation.
After Feature transformation we again Linear Regression model and found Adjusted_R^2 = 0.669 with MSE = 1.38 on cross validation set.

Next we applied ridge regression, Decision Tree, Random Forest and Support Vector Machine on train data and tuned it on cross validation set. 

Performance of Decision Tree on train and cross validation for different depth

![image](https://user-images.githubusercontent.com/76644910/125196095-1c13a580-e276-11eb-9a79-1954a6d91f05.png)

Performance of Random Forest on train & cross validation for different no. of features & max depth 9

![image](https://user-images.githubusercontent.com/76644910/125196120-33529300-e276-11eb-836a-f2d2bb5e6858.png)

Below table summarizes the performance of these models on cross validation set.

![image](https://user-images.githubusercontent.com/76644910/125196132-436a7280-e276-11eb-9312-6b99d1a45be3.png)

We found random forest performs best on cross validation set with MSE of 1.01.

**HYPERPARAMETER OPTIMIZATION USING BAYESIAN OPTIMIZATION**

We applied Bayesian Optimization and 5 fold cross validation to find best parameter for Random Forest.
In below table shows the range over which hyper parameters of Random Forest were varied for selection of best parameter.

![image](https://user-images.githubusercontent.com/76644910/125196216-a2c88280-e276-11eb-9602-0a5645bed872.png)

Best Set of Parameters for Random Forest

![image](https://user-images.githubusercontent.com/76644910/125196239-b8d64300-e276-11eb-9f85-05210253b551.png)

Finally we built Random Forest model on train and cross validation combined with best set of hyper parameter and tested it on test data.
We found train MSE =0.34 and test MSE = 1.16.
Next we built the Random forest with the same best set of forest on all data and deployed it locally using gradio library.

**Feature Importance**

![image](https://user-images.githubusercontent.com/76644910/125196253-ce4b6d00-e276-11eb-91c0-89f3222b30c8.png)

Top 5 most important features we found were V1 followed by V6, V7, V5 and V8.
Where V1 = Old_V0 (PC V0) = 0.015 * AT + 0.35 * AFDP + 0.44 * GTEP + 0.41 * TIT -0.33 * TAT + 0.45 * TEY + 0.45 * CDP

--
--

**Model Building Process of NOx**

Similar steps were followed to build model for NOx emission prediction.

**Feature Engineering**

**Principle Component Analysis**
Below figure represent how predictors were combined after PCA. VO, V1, V2, V3, V4, V5  are principle components we found after PCA

![image](https://user-images.githubusercontent.com/76644910/125196291-fb981b00-e276-11eb-8bd5-782188b69959.png)

V0, V1, V2, V3, V4 AND V5 are principle components obtained after PCA.

Each row represents the coefficient of linear combination for respective principle component.

Linear Regressing Model built on above described PCA showed Adjusted_R^2 = 0.38 with MSE = 81.13 on cross validation set. Linear regression model has very poor performance. 

**Polynomial Feature Transformation**
Below figure represent how features were combined after polynomial feature transformation.

![image](https://user-images.githubusercontent.com/76644910/125196325-23877e80-e277-11eb-943d-e72a21a0281e.png)

Example for how variables have combined

V0 = (Old_VO^0) * (Old_V1^0) * (Old_V2^0) * (Old_V3^0) * (Old_V4^0) * (Old_V5^0)

V1 = (Old_VO^1) * (Old_V1^0) * (Old_V2^0) * (Old_V3^0) * (Old_V4^0) * (Old_V5^0)

V7 = (Old_VO^2) * (Old_V1^0) * (Old_V2^0) * (Old_V3^0) * (Old_V4^0) * (Old_V5^0)

V8 = (Old_VO^1) * (Old_V1^1) * (Old_V2^0) * (Old_V3^0) * (Old_V4^0) * (Old_V5^0) ...... & soon

Old_Vi’s are principle components and Vi’s are new set of features after feature transformation.
After Feature transformation we again Linear Regression model and found Adjusted_R^2 = 0.596 with MSE = 52.81 on cross validation set.
Next we applied ridge regression, Decision Tree and Random on train data and tuned it on cross validation set. 

*Performance of Decision Tree on train and cross validation for different depth*

![image](https://user-images.githubusercontent.com/76644910/125196356-487bf180-e277-11eb-9362-608f3a5e4d72.png)

*Performance of Random Forest on train & cross validation for different no. of features & max depth 13*

![image](https://user-images.githubusercontent.com/76644910/125196389-66e1ed00-e277-11eb-9556-1eddcff1bf4e.png)

Below table summarizes the performance of these models on cross validation set.

![image](https://user-images.githubusercontent.com/76644910/125196407-79f4bd00-e277-11eb-8f18-3ee79f9da9d0.png)

We found random forest performs best on cross validation set with MSE of 26.78.

**HYPERPARAMETER OPTIMIZATION USING BAYESIAN OPTIMIZATION**
We applied Bayesian Optimization and 5 fold cross validation to find best parameter for Random Forest.
In below table shows the range over which hyper parameters of Random Forest were varied for selection of best parameter

![image](https://user-images.githubusercontent.com/76644910/125196439-97298b80-e277-11eb-81bf-7428a908265f.png)

**Best Set of Parameters for Random Forest**

![image](https://user-images.githubusercontent.com/76644910/125196457-a8729800-e277-11eb-86af-167fb6d631c0.png)

Finally we built Random Forest model on train and cross validation combined with best set of hyper parameter and tested it on test data.
We found train MSE = 3.23 and test MSE = 22.43
Next we built the Random forest with the same best set of forest on all data and deployed it locally using gradio library.

**Feature Importance**

![image](https://user-images.githubusercontent.com/76644910/125196475-c50ed000-e277-11eb-9625-781e53e074c1.png)

Top 5 most important features we found were V6 followed by V5, V9, V3 and V26.
Where V5 = Old_V4 (PC V4) = 0.28 * AT + 0.15 * AP + 0.12 * AH + 0.65 * AFDP - 0.14 * GTEP - 0.38 * TIT -0.47 * TAT - 0.24 * TEY - 0.13 * CDP.

**References & Citation**

Heysem Kaya, PÄ±nar TÃ¼fekci and ErdinÃ§ Uzun. 'Predicting CO and NOx emissions from gas turbines: novel data and a benchmark PEMS', Turkish Journal of Electrical Engineering & Computer Sciences, vol. 27, 2019, pp. 4783-4796


x-----------------------x-----------------------x------------------------x-----------------------x----------------------------x
