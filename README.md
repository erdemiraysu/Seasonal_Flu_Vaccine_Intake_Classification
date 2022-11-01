# Predict Seasonal Flu Vaccines Project3


## Overview
***
- **CDC wants to understand the leading factors in determining whether a person would take the sesoanal flu vaccine so that they could focus on the right strategies for their public efforts and vaccination campaigns to educate the public, raise awareness and maximize vaccine intake.**

- They also want to know the likelihood to receive the seasonal flu vaccine for specific demographic groups and have feedback about whether their efforts are successfull. 

- **GOAL**: is build a classifier to predict seasonal flu vaccination status using information they shared about their backgrounds, opinions, and health behaviors. My main purpose was to make predictions as accurately as possible while balancing between sensitivity and specificity.

## Business and Data Understanding
***
* The data was obtained from the **National 2009 H1N1 Flu Survey** provided at [DrivenData](https://www.drivendata.org/competitions/66/flu-shot-learning/). 

* This phone survey contained dfata from 26707 particiants, and asked people whether they had received H1N1 and seasonal flu vaccines, in conjunction with information they shared about their lives, opinions, and behaviors. 

* In this project I will be focusing on `seasonal flu` only and information regarding individuals' opinions about the H1N1 vaccine were excluded from the analyses. The relevant variables/features included in the dataset are:

**Target Feature**: 
* `seasonal_vaccine` - Whether respondent received seasonal flu vaccine or not.

**Predictive Features**:

* `behavioral_antiviral_meds` - Has taken antiviral medications. (binary)
* `behavioral_avoidance` - Has avoided close contact with others with flu-like symptoms. (binary)
* `behavioral_face_mask` - Has bought a face mask. (binary)
* `behavioral_wash_hands` - Has frequently washed hands or used hand sanitizer. (binary)
* `behavioral_large_gatherings` - Has reduced time at large gatherings. (binary)
* `behavioral_outside_home` - Has reduced contact with people outside of own household. (binary)
* `behavioral_touch_face` - Has avoided touching eyes, nose, or mouth. (binary)
* `doctor_recc_seasonal` - Seasonal flu vaccine was recommended by doctor. (binary)
* `chronic_med_condition` - Has any of the following chronic medical conditions: asthma or an other lung condition, diabetes, a heart condition, a kidney condition, sickle cell anemia or other anemia, a neurological or neuromuscular condition, a liver condition, or a weakened immune system caused by a chronic illness or by medicines taken for a chronic illness. (binary)
* `child_under_6_months` - Has regular close contact with a child under the age of six months. (binary)
* `health_worker` - Is a healthcare worker. (binary)
* `health_insurance` - Has health insurance. (binary)
* `opinion_seas_vacc_effective` - Respondent's opinion about seasonal flu vaccine effectiveness. 1 = Not at all effective; 2 = Not very effective; 3 = Don't know; 4 = Somewhat effective; 5 = Very effective.
* `opinion_seas_risk` - Respondent's opinion about risk of getting sick with seasonal flu without vaccine. 1 = Very Low; 2 = Somewhat low; 3 = Don't know; 4 = Somewhat high; 5 = Very high.
* `opinion_seas_sick_from_vacc` - Respondent's worry of getting sick from taking seasonal flu vaccine. 1 = Not at all worried; 2 = Not very worried; 3 = Don't know; 4 = Somewhat worried; 5 = Very worried. 
* `age_group` - Age group of respondent.
* `education` - Self-reported education level.
* `race` - Race of respondent.
* `sex` - Sex of respondent.
* `income_poverty` - Household annual income of respondent with respect to 2008 Census poverty thresholds.
* `marital_status` - Marital status of respondent.
* `rent_or_own` - Housing situation of respondent.
* `employment_status` - Employment status of respondent.
* `hhs_geo_region` - Respondent's residence using a 10-region geographic classification defined by the U.S. Dept. of Health and Human Services. Values are represented as short random character strings.
* `census_msa` - Respondent's residence within metropolitan statistical areas (MSA) as defined by the U.S. Census.
* `household_adults` - Number of other adults in household, top-coded to 3.
* `household_children` - Number of children in household, top-coded to 3.
* `employment_industry` - Type of industry respondent is employed in. Values are represented as short random character strings.
* `employment_occupation` - Type of occupation of respondent. Values are represented as short random character strings.


## Data Cleaning:
***
* Columns (variables) with more than 50% of the data missing were dropped (`emplyment_occupation` and `empltment_industry`). 
* Rows (participants) with at least  1/3rd of the data missing were dropped (total of 761 people out of 26707). 
* Null values for the two important variables (`heath_insurance` and `income_poverty`) which comprised %43 and %13 of the data, were imputed using a predcitive modeling approach. 
* Below graph shows the data matrix with null values before and after data cleaning:

![DataMatrix_BeforeAfterCleaning](https://user-images.githubusercontent.com/61121277/199284666-c8f26292-406a-43c3-a6dd-36a780364683.png)

## Preprocessing
***
#### Binary (yes/no) Columns:
* Many of the variables in float type are actually binary (yes/no).
* Given that the proportion of null values are not too high for these variables, the null values will be replaced with the **most frequent**. 

    ##### `health_insurance`:
    * A **predictive model** will be used to impute the missing values and then these values will be merged into the dataset. 

#### Numerical Columns:
* Some of variables in float type are **ordinal** (some sense of ordering to its categories), so they will be treated as **numerical**. 
* The null values will be replaced with the **Median**. 

#### Categorical Columns:
* The variables in object type are **nominal** (no intrinsic ordering to its categories), so they will be treated as **categorical**. 
* The null values will be replaced with a **contant('missing')** creating its own level before one-hot encoding these variables. 

    ##### `income_poverty`:
    * A **predictive model** will be used to impute the missing values and then these values will be merged into the dataset. 

## Modeling
***
1. The data was split into training and test sets.
2. The data was pre-processed. 
3. Several types of classifiers were built, tuned (using GridSearchCV to test combinations of hyperparameters) and validated:

    - Logistic Regression
    - Decision Tree
    - Random Forest
    - XGradient Boosted
    - Stacking Classifier (using above models)

4. Scoring Metric: Roc_Auc was used afor tuning hyperparameters and evaluating model performance, because:
 
* We care equally about true positives and true negatives, and the roc curve gives a desirable balance between **sensitivity/recall (maximizing True positive Rate)** and and **1 - specificity  (minimizing False Positive Rate - Probability that a true negative will test positive)**

* We want to utilizes **"probabilities"** of class prediction. Based on this, we’re able to more precisely evaluate and compare the models. 

## Evaluation
***




![Compare_RocCurve_Models](https://user-images.githubusercontent.com/61121277/199292751-bfc0ff45-8ff0-49d0-917f-2224ba3c2ee6.png)
* **XGboost** gives the best performance on both train (tells if model is confident in it’s learning) and test datasets (tells if the results are negeralizable to an unknown dataset). 

![XGBoost_Results_1](https://user-images.githubusercontent.com/61121277/199292820-e56259e2-b6a1-4be8-ad3f-5f213c7375d1.png)
![XGBoost_Results_2](https://user-images.githubusercontent.com/61121277/199292974-b6ed5864-3e66-49b0-b4bd-ef695d94705d.png)
* Results from the best fitting model gives an Accuracy score of 79%, Sensitivity/Recall score of 79% and a Specificity scores of 82%.

![XGBoost_FeatureImportance](https://user-images.githubusercontent.com/61121277/199292805-566c278c-e1e8-4a4a-b643-044569ce0812.png)
The most important 6 features in predciting whether a person would get the seasonal vacccine are:

- `doctor_recc_seasonal`
- `healht_insurance`
- `opinion_seas_vacc_effective`  
- `opinion_seas_risk`
- `age_group_65+ Years`
- `health_worker` 

## Conclusion
***

![MostImportantFeatures_Probability_BarPlot](https://user-images.githubusercontent.com/61121277/199118595-397eb549-3f7b-417e-8e9a-52b583765cc4.png)

You are more likely to get the vaccine if:

- your doctor recommends the vaccine
- you have health insurance
- you think the vaccine is effective
- you think you can get sick from flu
- you are older
- you are a health worker
   
## Recommendations
***
* Target physicians by educating them on the importance of vaccination &  recommending it to their patients!
* Target uninsured populations in the campaign, but better yet work on universal health coverage.
* Inform the people about the effectiveness and safety of the vaccine and their risk of falling ill and developing complications if not vaccinated.
* As a priority keep focusing your campaign on older age groups, because they are at more risk of developing flu-related complications compared to younger age groups, and there is still room to progress even for those +65. But also target younger people as a key demographic population since their vaccination rates are much lower.

## Next Steps
***
* Encrypted employment industry, employment occupation, and geographical region info, hard to make any specific suggestions based on these features. 
* Results on health insurance are not very reliable due to %40 of the data being null and being encoded using predictive modeling. More emphasis needs to be given to this variable next time the survey is conducted even it is a significant feature in predicting vaccine outcome. 
* More recent data needs to be collected after the Covid-19 pandemic since the pandemic might have altered people’s attitude towards flu vaccine as well. 

## Repository Structure
    .
    ├── images 
    ├── data 
    ├── Notebook.ipynb     
    ├── Notebook.pdf 
    ├── Presentation.pdf                                             
    └── README.md   

## Contact Info:
* Email: erdemiraysu@gmail.com
* GitHub: [@erdemiraysu](https://github.com/erdemiraysu/)
* [LinkedIn](https://www.linkedin.com/in/aysuerdemir)
