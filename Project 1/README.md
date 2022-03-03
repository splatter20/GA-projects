## Problem Statement
---
As a guidance counselor in a high school, students are stressed over being able entering college. Students would ask if they should take SATs or ACTs to enter into a college.

In this project, I would like to explore if taking SATs or ACTs would be easier for students to enter colleges.

---
## Data Sets Used
---

Provided data sets: sat_2017, sat_2018, act_2017, act_2018, sat_act_by colleges
Number of ACT and SAT test takers were referenced from: 
ACT: https://www.edweek.org/teaching-learning/math-scores-slide-to-a-20-year-low-on-act/2018/10 

SAT: https://reports.collegeboard.org/archive/sat-suite-program-results/2018/class-2018-results 

---
## Data Dictionary
---

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**state**|*object*|sat_2017, sat_2018, sat_2019, act_2017, act_2018| The name of the state of interest|
|**participation**|*float*|sat_2017, sat_2018, sat_2019, act_2017, act_2018| The percent of graduating high school students who took the exam (act/sat respectively)( units percent to two decimal places, 0.38 means 38% )
|**ebrw**|*interger*|sat_2017, sat_2018, sat_2019, sat_2019_by_major| The average score of Evidence-Based Reading and Writing (ebrw) in sat for the state|
|**math**|*interger*|sat_2017, sat_2018, sat_2019, sat_2019_by_major| The average score of Math in sat for the state|
|**total**|*integer*|sat_2017, sat_2018, sat_2019, sat_2019_by_major| The average combined score of ebrw and math in sat for the state|
|**composite**|*integer*|act_2017, act_2018| The average combined score in act for the state|
|**school**|*object*|sat_act_by_college| The name of the school of interest|
|**number of applicants**|*integer*|sat_act_by_college| The total number of applicants to the school for both act and sat|
|**accept rate**|*float*|sat_act_by_college| The percent of accepted students out of the number of applicants ( units percent to two decimal places, 0.38 means 38% )
|**sat 25th percentile**|*float*|sat_act_by_college| The combined sat score for the 25th percentile of students who were accepted based on sat.|
|**sat 75th percentile**|*float*|sat_act_by_college| The combined sat score for the 75th percentile of students who were accepted based on sat.|
|**act 25th percentile**|*float*|sat_act_by_college| The combined act score for the 25th percentile of students who were accepted based on act.|
|**act 75th percentile**|*float*|sat_act_by_college| The combined act score for the 75th percentile of students who were accepted based on act.|
|**type**|*object*|total_overall_participation| The type of test taken (SAT or ACTs)|
|**test takers**|*integer*|total_overall_participation| The number of high school students who had taken SATs or ACTs|

---
## Executive Summary
---

This project seeks to compare the SAT and ACT average scores by state for 2017 and 2018 with the admissions for various colleges.

Exploratory data analysis seems to have showed a disparity for admissions into college based on SAT and ACT scores. Based on the 25th percentile of students accepted into colleges, more students had achieved the required scores to enter the colleges for SAT compared to ACT. 

Based on analysis of the participation rates, ACT seems to be the more popular choice with 16-17 states having mandatory ACT tests compared to 4-5 states having mandatory SAT tests. However, upon further investigation with number of test takers for both SAT and ACT, it can be seen that both SAT and ACT are around the same.

---
## Methodology
---

The raw data sets were first analysed for any potential issues and subsequently ironed out the identified issues by removing unwanted values, standardising and renaming columns and converting values into the proper format.

Exploratory data analysis was conducted on the cleaned data sets to explore on the problem statement posed, gathering the various statistics such as mean and standard deviation of the data. Data visualisation was then used to observe any trends which may lead to a conclusion. After spotting the trend, recommendations can then be made, addressing the problem statement.


---
## Conclusion and Recommendation  
---

As a guidance counselor, I would recommend graduating high school students to take SAT over ACT.

However, students should still focus on ACT if the state mandates taking ACT and only attempt to take the SAT if they are confident in splitting their attention

It is also recommended for colleges to review their admissions as there is an apparent disparity between the acceptance of SAT scores vs ACT scores.

*Future areas of investigations*
- The number of students accepted by Colleges with SAT scores or ACT scores or both
- Whether the college degrees would also have a disparity in acceptance for SAT and ACT scores.