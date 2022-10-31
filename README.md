# Predict Seasonal Flu Vaccines Project3

## Overview
***
- **CDC wants to understand the leading factors in determining whether a person would take the sesoanal flu vaccine so that they could focus on the right strategies for their public efforts and vaccination campaigns to educate the public, raise awareness and maximize vaccine intake.**

- They also want to know the likelihood to receive the seasonal flu vaccine for specific demographic groups and have feedback about whether their efforts are successfull. 

- My goal is build a classifier to predict seasonal flu vaccination status using information they shared about their backgrounds, opinions, and health behaviors. My main purpose was to make predictions as accurately as possible.

## Business and Data Understanding
***
* The data was obtained from the **National 2009 H1N1 Flu Survey** provided at [DrivenData](https://www.drivendata.org/competitions/66/flu-shot-learning/). This phone survey asked people whether they had received H1N1 and seasonal flu vaccines, in conjunction with information they shared about their lives, opinions, and behaviors. 


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
![DataMatrix_BeforeAfterCleaning](https://user-images.githubusercontent.com/61121277/199094926-05f3df1b-7487-45fd-a879-da41d8edff10.png)


## Preprocessing
***
### Binary Columns:
* Many of variables in float type are actually **binary (yes/no)**. 
* Given that the proportion of null values are not too high for these variables, the null values will be replaced with the **most frequent**. 

    #### `health_insurance`:
    * This variable will be treated as **binary (yes/no)**.
    * A **predictive model** will be used to impute the missing values and then these values will be merged into the dataset. 

### Numerical Columns:
* Some of variables in float type are **ordinal** (some sense of ordering to its categories), so they will be treated as **numerical**. 
* The null values will be replaced with the **Median**. 

### Categorical Columns:
* The variables in object type are **nominal** (no intrinsic ordering to its categories), so they will be treated as **categorical**. 
* The null values will be replaced with a **contant('missing')** creating its own level before one-hot encoding these variables. 

    #### `income_poverty`:
    * This variable will be treated as **categorical**.
    * A **predictive model** will be used to impute the missing values and then these values will be merged into the dataset. 



## Modeling
***
1. The dataset was cleaned and engineered.
2. The data was split into training and test sets.
3. The data was pre-processed. 
4. Several types of classifiers were built, tuned (using GridSearchCV to test combinations of hyperparameters) and validated:

    - Logistic Regression
    - Decision Tree
    - Random Forest
    - XGradient Boosted
    - Stacking Classifier (using above models)

Roc_Auc was used as the scoring metric for tuning hyperparameters and evaluating model performance. 


## Evaluation
***










## Conclusion
***
**You are more likely to get the vaccine if:**

   - your doctor recommends the vaccine
   - you have health insurance
   - you think the vaccine is effective
   - you think you can get sick from flu
   - you are older
   - you are a health worker
   - 
## Recommendations
***
* Target physicians by educating them on the importance of vaccination &  recommending it to their patients!
* Target uninsured populations in the campaign, but better yet work on universal health coverage for all individuals and communities.
* Focus your campaign on informing the people about the effectiveness and safety of the vaccine or their risk of falling ill and developing complications if not vaccinated. 
* As a priority keep focusing your campaign on older age groups, because they are at more risk of developing flu-related complications compared to younger age groups.But also target younger people as a key demographic population to maximize the benefits of herd immunity since their vaccination rates are much lower.

## Next Steps
***
* Encrypted employment industry, employment occupation, and geographical region info, hard to make any specific suggestions based on these features. 
* Results on health insurance are not very reliable due to %40 of the data being null and being encoded using predictive modeling. More care needs to be given to this variable next time the survey is conducted. 
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
