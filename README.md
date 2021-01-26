# Capstone Project

#Link to the screencast video on YouTube 

#Project Overview

This is the capstone project as part of Azure Nanodegree Program, Machine Learning Engineer with Microsoft Azure.

As required by the project we have selected "Heart failure clinical records" data set (details section below) and performed machine learning task of predicting survival of patients facing heart failure (binary classification ) using 12 feautures identified in the data set. 

As per the project guidance we created two experiments, one using Automated ML (AutoML) and another model using Scikit Learn Logistic Regression classifier, whose hyperparameters were tuned using HyperDrive

From each experiment we selected one best model based on "accuracy" metric. 

Details are: 

i) AutoML best model: 

ii) HyperDr

Based on comparison of two models we selected --- model from AutoML eperiment and then deployed it as a webservice (REST API). We then tested the webservice by sending a request to the model endpint.



#Dataset used

We have used Heart failure clinical records data set as published on "UCI Machine Learning Repository"and "Kaggle Heart Failure Prediction" competion. 

This data set has been published as part of folowing paper: Davide Chicco, Giuseppe Jurman: "Machine learning can predict survival of patients with heart failure from serum creatinine and ejection fraction alone". BMC Medical Informatics and Decision Making 20, 16 (2020).

This dataset contains the medical records of 299 heart failure patients collected at the Faisalabad Institute of Cardiology and at the Allied Hospital in Faisalabad (Punjab, Pakistan), during April–December 2015 [52, 66]. The patients consisted of 105 women and 194 men, and their ages range between 40 and 95 years old (Table 1). All 299 patients had left ventricular systolic dysfunction and had previous heart failures that put them in classes III or IV of New York Heart Association (NYHA) classification of the stages of heart failure.

The dataset contains 13 features, which report clinical, body, and lifestyle information, that we briefly describe here.

- Age: age of the patient (years)
- Anaemia: decrease of red blood cells or hemoglobin (boolean)
- High blood pressure: if the patient has hypertension (boolean)
- Ceatinine phosphokinase (CPK): level of the CPK enzyme in the blood (mcg/L)
- Diabetes: if the patient has diabetes (boolean)
- Ejection fraction: percentage of blood leaving the heart at each contraction (percentage)
- Platelets: platelets in the blood (kiloplatelets/mL)
- Sex: woman or man (binary)
- Serum creatinine: level of serum creatinine in the blood (mg/dL)
- Serum sodium: level of serum sodium in the blood (mEq/L)
- Smoking: if the patient smokes or not (boolean)
- Time: follow-up period (days)
- [target] Death event: if the patient deceased during the follow-up period (boolean)


#Data import into Azure ML Studio workspace.

We have source data set as a csv file from kaggle competion [Kaggle!](https://www.kaggle.com/andrewmvd/heart-failure-clinical-data). 

We uploaded this file into our workspace and then uploaded it into our deafult datastore. From their convert this file into Tabular data set for our AUtoML eperiment purposes.

For our hyperdrive expermient, we read data as a pandas dataframe into our experiment.

#AutoML experiment: settings and configuration

AutoML experiment was configured using folloing setting:

- 4 concurrent iterations of models.
- primary metric as "accuracy".
- machine learning task as "Classification". 
- Automatic feature selection by AutoML.
- Early stopping enabled.


#Hyperparameter search: types of parameters and their ranges



#Two models with the best parameters

i) From AutoML experiment best model selected was VotingEnsemble with _ _ % accuracy. Details of its parameters are as follows:


ii) From Sci-kit Learn trained model , tuned with Hyperdrive, best model was  ----- with - - % accuracy. Details of its parameters are as follows:


#Deployed model and instructions on how to query the endpoint with a sample input

Based on higher accuracy metric produced, we selected VotingEnsemble model produced by AutoML experiment for deployment. 
In order to deploy it , we first registerd the model and provided it an environment for deployment. We took advantage of Azure provided environment "AzureML-AutoML" . 
We set up Inference Configuration and provided it with a scoring file, this file contained API model (i.e fields that API would need for data interchange).
We then deployed the model using Azure Container Instance Webservices (Aci). Deployment enabled a REST API that prvide scoring uri with keys for authentication. 
We passed test data inform of Json load to webservice configured and it validated our deployment by providing a response in expected format (1,0)


#How to improve the project in the future

We can suggest following improvments that may result in better model or faster model deployment:

i) Use more powerful computer cluster such as GPU instanced with more nodes. This may enable increase in concurrent iterations.

ii) Data has class imbalance with many 1/3 deaths events vs 2/3 non deaths events. We might address it by procuring more data.

iii) We need to assess Classifiers that AutoML has not tested and hyperparameters that are not configured. We might further wish to train our data using those model and parameters by using hyperdrive run and experiment with a different set of parameters.

iv) In Hyperdrive experimnet test more classifiers including some of ensemble classifiers as identified by AutoML. This might improve model performance by identifying a faster and more accurate model. 

v) In Hyperdrive experiment use Bayesian Parameter sampling: This might make experiment run faster and be able to quickly identify best hyperparameter.

vii) In Hyperdrive experiment test more hyperparameter for tuning such as penalty, solver, class_weight etc. They might improve model performance by testing a hyperparameter combination that is able to yield more accurate model.

iv) In Hyperdrive pipeline to address class imbalance in data by either using SMOTE resampling technique or using class_weight parameter.


#ALL the screenshots required with a short description

i) AutoML Model: 

-screenshot of the RunDetails widget that shows the progress of the training runs of the different experiments.
-screenshot of the best model with its run id.

ii) Hyperdrive Model:

-creenshot of the RunDetails widget that shows the progress of the training runs of the different experiments.
-a screenshot of the best model with its run id and the different hyperparameters that were tuned.

Deploying the Model:
-screenshot showing the model endpoint as active.




