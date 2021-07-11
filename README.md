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

Linear Regressing Model built on above described PCA showed Adjusted_R^2 = 0.57 with MSE = 1.78 on cross validation set.

**Polynomial Feature Transformation**
Next we applied *Polynomial Feature transformation to get new features as a combination of old*
Below figure represent how features were combined after polynomial feature transformation

![image](https://user-images.githubusercontent.com/76644910/125196034-e4a4f900-e275-11eb-86bf-7ade9cab02c2.png)

Old_Vi’s are principle components and Vi’s are new set of features after feature transformation.
After Feature transformation we again Linear Regression model and found Adjusted_R^2 = 0.669 with MSE = 1.38 on cross validation set.






