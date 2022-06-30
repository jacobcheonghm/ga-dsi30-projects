# Project 1: Standardized Test Analysis

## Problem Statement
#### DreamCollege's Challenge
DreamCollege is a private tutoring company providing tutoring and consultation services to high school students, helping them ace the ACT and/or SAT and consequently earn themselve admission to their dream college.

Being a start-up, DreamCollege would like to concentrate their resouces and efforts on a few select states in order to build their reputatio. With the change in test format and state requirements for the 2 standardized test, DreamCollege wants to understand how the changes affect the trend on popularity of the test in the various states. This will help the executive team to decide on how and where to better market DreamCollege.

#### Background on ACT and SAT
The SAT and ACT are standardized tests that many colleges and universities in the United States require for their admissions process. This score is used along with other materials such as grade point average (GPA) and essay responses to determine whether or not a potential student will be accepted to the university.

The SAT has two sections of the test: Evidence-Based Reading and Writing and Math ([*source*](https://www.princetonreview.com/college/sat-sections)). The ACT has 4 sections: English, Mathematics, Reading, and Science, with an additional optional writing section ([*source*](https://www.act.org/content/act/en/products-and-services/the-act/scores/understanding-your-scores.html)). They have different score ranges, which you can read more about on their websites or additional outside sources (a quick Google search will help you understand the scores for each test):
* [SAT](https://collegereadiness.collegeboard.org/sat)
* [ACT](https://www.act.org/content/act/en.html)

Standardized tests have long been a controversial topic for students, administrators, and legislators. Since the 1940's, an increasing number of colleges have been using scores from sudents' performances on tests like the SAT and the ACT as a measure for college readiness and aptitude ([*source*](https://www.minotdailynews.com/news/local-news/2017/04/a-brief-history-of-the-sat-and-act/)). Supporters of these tests argue that these scores can be used as an objective measure to determine college admittance. Opponents of these tests claim that these tests are not accurate measures of students potential or ability and serve as an inequitable barrier to entry. Lately, more and more schools are opting to drop the SAT/ACT requirement for their Fall 2021 applications ([*read more about this here*](https://www.cnn.com/2020/04/14/us/coronavirus-colleges-sat-act-test-trnd/index.html)).

## Data Dictionary

1. Datasets used in the study.
    
| **No.** | **Dataset Name** | **Description**          |
|---------|------------------|--------------------------|
| 1       | act_2017.csv     | 2017 ACT Scores by State |
| 2       | act_2018.csv     | 2018 ACT Scores by State |
| 3       | act_2019.csv     | 2019 ACT Scores by State |
| 4       | sat_2017.csv     | 2017 SAT Scores by State |
| 5       | sat_2018.csv     | 2018 SAT Scores by State |
| 6       | sat_2019.csv     | 2019 SAT Scores by State |

2. Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|act_XX, sat_XX|The states is US where results from where the test results was collected|
|participation|float|act_XX, sat_XX|Participation rate of respective test|
|composite|float|act_XX|Average of the English, Math, Reading and Science score for ACT|
|ebrw|int|sat_XX|Average score for Evidence-Based Reading and Writing component of the SAT|
|math|int|sat_XX|Average score for Math component of the SAT|
|total|int|sat_XX| Sum of the EBRW and Math components of the SAT test| 

## Summary of Analysis

### 1. Summary Statistics


Mean participation for ACT has been consistently decreasing from 0.65 in 2017, 0.62 in 2018 and finally 0.58 on 2019. That is in contrast ot the increasing participation rate for SAT at 0.40, 0.46 and 0.49 for years 2017, 2018 and 2019 respectively. However mean participation rate for ACT is still higher than SAT in all three years.

We can also infer that more states have compulsory ACT requirements as the 75% quartile for the participation in all years stays at 1.00 while despite a increasing 75% quartile for SAT participation through the year, it fails to reach 1.00.

Both means for ACT composite and SAT total score also follows a gradual downward trend.

### 2. ACT & SAT Participation Rate 2017-2019

|    |          state | 2017 |   |          state | 2018 |   |          state | 2019 |
|---:|---------------:|-----:|--:|---------------:|-----:|--:|---------------:|-----:|
|  1 |        Alabama |  1.0 |   |        Alabama |  1.0 |   |        Alabama |  1.0 |
|  2 |       Arkansas |  1.0 |   |       Arkansas |  1.0 |   |       Arkansas |  1.0 |
|  3 |       Colorado |  1.0 |   |       Kentucky |  1.0 |   |       Kentucky |  1.0 |
|  4 |       Kentucky |  1.0 |   |      Louisiana |  1.0 |   |      Louisiana |  1.0 |
|  5 |      Louisiana |  1.0 |   |    Mississippi |  1.0 |   |    Mississippi |  1.0 |
|  6 |      Minnesota |  1.0 |   |       Missouri |  1.0 |   |        Montana |  1.0 |
|  7 |    Mississippi |  1.0 |   |        Montana |  1.0 |   |       Nebraska |  1.0 |
|  8 |       Missouri |  1.0 |   |       Nebraska |  1.0 |   |         Nevada |  1.0 |
|  9 |        Montana |  1.0 |   |         Nevada |  1.0 |   | North Carolina |  1.0 |
| 10 |         Nevada |  1.0 |   | North Carolina |  1.0 |   |           Ohio |  1.0 |
| 11 | North Carolina |  1.0 |   |           Ohio |  1.0 |   |       Oklahoma |  1.0 |
| 12 |       Oklahoma |  1.0 |   |       Oklahoma |  1.0 |   |      Tennessee |  1.0 |
| 13 | South Carolina |  1.0 |   | South Carolina |  1.0 |   |           Utah |  1.0 |
| 14 |      Tennessee |  1.0 |   |      Tennessee |  1.0 |   |      Wisconsin |  1.0 |
| 15 |           Utah |  1.0 |   |           Utah |  1.0 |   |        Wyoming |  1.0 |
| 16 |      Wisconsin |  1.0 |   |      Wisconsin |  1.0 |   |                |      |
| 17 |        Wyoming |  1.0 |   |        Wyoming |  1.0 |   |                |      |

States with 100% participation rate for ACT.

In 2017, with the exception of **Arkansas** (ACT offered for free), **Colorado**, **Minnesota**, **Oklahoma** (require either SAT or ACT), **Tennessee** (require either SAT or ACT), taking ACT is mandatory in the above states.

Again in 2018, we observe 17 states with 100% participation in ACT. **Colorado** has dropped out of this list while **Ohio** (require either ACT or SAT) was added to it.

For year 2019, states that have 100% participation in ACT dropped to 15. **South Carolina** and  **Missouri** are no longer included in this list.

|   |            **State** | **2017** |   |   **State** | **2018** |   |    **State** | **2019** |
|--:|---------------------:|---------:|--:|------------:|---------:|--:|-------------:|---------:|
| 1 |          Connecticut |      1.0 |   |    Colorado |      1.0 |   |     Colorado |      1.0 |
| 2 |             Delaware |      1.0 |   | Connecticut |      1.0 |   |  Connecticut |      1.0 |
| 3 | District of Columbia |      1.0 |   |    Delaware |      1.0 |   |     Delaware |      1.0 |
| 4 |             Michigan |      1.0 |   |       Idaho |      1.0 |   |      Florida |      1.0 |
| 5 |                      |          |   |    Michigan |      1.0 |   |        Idaho |      1.0 |
| 6 |                      |          |   |             |          |   |     Illinois |      1.0 |
| 7 |                      |          |   |             |          |   |     Michigan |      1.0 |
| 8 |                      |          |   |             |          |   | Rhode Island |      1.0 |

States with 100% participation rate for SAT.

For year 2017, we observe the above 4 states with 100% participation in SAT.

For year 2018, we see the inclusion of **Colorado** and exclusion of **District of Columbia** in the list of states with 100% SAT.

In 2019, we see the inclusion of more states to the list of states with 100% SAT participation, they include **Florida**, **Illinois** and **Rhode Island**.

|                               | **2017**      | **2018**     | **2019**            |
|-------------------------------|---------------|--------------|---------------------|
| **ACT Highest Participation** | North Dakota  | Minnesota    | North Dakota        |
| **ACT Lowest Participation**  | Maine         | Maine        | Maine               |
| **SAT Highest Participation** | New Hampshire | Maine        | Maine, West Virginia |
| **SAT Lowest Participation**  | North Dakota  | North Dakota | North Dakota        |

States with the highest (excluding 100% participation states) and lowest participation for each test.

|   | **State** | **ACT 2017** | **SAT 2017** |   |      **State** | **ACT 2018** | **SAT 2018** |   |      **State** | **ACT 2019** | **SAT 2019** |
|--:|----------:|-------------:|-------------:|--:|---------------:|-------------:|-------------:|--:|---------------:|-------------:|-------------:|
| 1 |   Florida |         0.73 |         0.83 |   |        Florida |         0.66 |         0.56 |   |        Florida |         0.54 |         1.00 |
| 2 |   Georgia |         0.55 |         0.61 |   |        Georgia |         0.53 |         0.70 |   |         Hawaii |         0.80 |         0.54 |
| 3 |    Hawaii |         0.90 |         0.55 |   |         Hawaii |         0.89 |         0.56 |   | North Carolina |         1.00 |         0.51 |
| 4 |           |              |              |   | North Carolina |         1.00 |         0.52 |   | South Carolina |         0.78 |         0.68 |
| 5 |           |              |              |   | South Carolina |         1.00 |         0.55 |   |                |              |              |

**Florida** and **Hawaii** are the two states that consistently achieve more than 50% participation rate in both test for all 3 years. **Georgia** featured in both 2017 and 2018, while **North Carolina** and **South Carolina** featured in 2018 and 2019 list of states that acheive more than 50% participation rate for both test.

### ACT and SAT Highest Scoring States

|               |         **2017 ACT**        |        **2018 ACT**       |        **2019 ACT**        |
|---------------|:---------------------------:|:-------------------------:|:--------------------------:|
| **State**     | New Hampshire               | Connecticut               | Connecticut, Massachusetts |
| **Composite** | 25.5                        | 25.6                      | 25.5                       |
|               | **2017 SAT**                | **2018 SAT**              |        **2019 SAT**        |
| **State**     | Minnesota                   | Minnesota                 | Minnesota                  |
| **Total**     | 1295                        | 1298                      | 1284                       |

Connecticut acheived the highest average composite ACT score the 2018 and 2019, it is joined by Massachusetts in 2019 and preceded by New Hampshire in 2017.

While in the case of SAT, Minnesota has consistently been acheiving the highest average total scores for all 3 years.

### 

<img src="../images/sat_act_heatmap.jpg"
     style="float: left; margin-right: 10px;" />

From the heatmap we can observe strong correlation for test partipation rate with test participation rate of previous years.
We can also seea strong negative correlation between test participation rate and test results.

 
<img src="../images/sat_act_average_score_hist.jpg"
     style="float: left; margin-right: 10px;" />
     
From the above histograms, we can observe bimodal distribution for the average test scores acheived in different states. The first peak(lower score) leans closer to the mean line as compared to the second peak(higher score).

<img src="../images/sat_act_boxplot.jpg"
     style="float: left; margin-right: 10px;" />
     
From the above boxplots, we can observe a contrasting change in participation rate from 2017 to 2019 between ACT and SAT. From the first 3 boxplots, we can observe a decreasing median as the year progess, while the upper quartile range have held relatively stable. In contrast, for the last 3 boxplots, we observe a increasing median and upper quartile range as the years progress.

<img src="../images/sat_act_correlation.jpg"
     style="float: left; margin-right: 10px;" />
     
From the above 6 scatterplots, we can observe a negative relationship between participation rate and average scored acheived.
This observation is consistent for both ACT and SAT and for years 2017 through 2019. Higher scores for either test are concentrated in areas with low participation, we can infer that minority of students who choose to take SAT are those who expect themself to do well.

<img src="../images/sat_ebrw_vs_math.jpg"
     style="float: left; margin-right: 10px;" />

The above boxplot shows that students who take the SAT typically does better for EBRW component. We observe the median, upper and lower quartile have been consistently higher than the math component for the 3 years.


## Conclusions & Recommendations
In conclusion, we can summarise the above data and analysis into a few key findings:

1. SAT is gaining popularity as we observe the trend of states switching from using ACT to SAT as the standardized test.

2. As of 2019, the states are still quite evenly split between SAT and ACT. 

3. Students who that SATs fare better for their EBRW component.

We will recommend DreamCollege to invest more resources in developing SAT centric product and services. We can expect services such as tutoring and consultation in how to optimize their score in SAT to be in demand especially in the state of Colorado and Illinois that have recently switched over from the ACT.

DreamcCollege can consider hiring more consultants and tutors that are more experienced in SAT to handle the expected increase in demand. They can also focus their marketing and communications effort in Colorado and Illinois where the SAT is still relatively novel.

Currently, we also would not advise DreamCollege to scale down their ACT centric resources and talents drastically as despite the increasing trend for states to adopt SAT, almost half the states still prefers ACT to SAT. The market and opportunity still exist so DreamCollege should still monitor the situation before downsizing their ACT department.

Despite the availability of free online test prep since 2015, improvements in the either of the SAT components have not been observed from 2017 through 2019. This may point to the demand for more personalized coaching tutoring to help students ace the SAT. As Dreamcollege venture into the SAT space, they can position themselves as the math specialist to get more attention since more students struggle with the math component of SAT.

### Sources and Citations

https://www.act.org/

https://satsuite.collegeboard.org/sat

https://www.princetonreview.com/college/sat-act

https://magoosh.com/hs/sat/states-that-require-the-act-or-sat/