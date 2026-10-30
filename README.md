# Social_Media_Students_Dashboard 
## Add calculated columns and measures
### Column 1: Usage Band 
Usage Band =
SWITCH(
    TRUE(),
    Students[Daily_Usage_Hours] < 3, "1. Low (<3h)",
    Students[Daily_Usage_Hours] < 5, "2. Moderate (3-5h)",
    Students[Daily_Usage_Hours] < 8, "3. High (5-8h)",
    "4. Very High (8h+)"
)
### Column 2: Sleep Band
Sleep Band =
SWITCH(
    TRUE(),
    Students[Sleep_Duration_Hours] < 6, "1. Under 6h",
    Students[Sleep_Duration_Hours] < 7, "2. 6-7h",
    Students[Sleep_Duration_Hours] < 8, "3. 7-8h",
    "4. 8h+"
)
### Column 3: Age Group
Age Group =
SWITCH(
    TRUE(),
    Students[Age] <= 17, "15-17",
    Students[Age] <= 20, "18-20",
    "21+"
)
### Column 4: Late Night Use
Late Night Use = IF(Students[Late_Night_Usage] = TRUE(), "Yes", "No")

### Column 5: Comparison Sort
Comparison Sort =
SWITCH(
    Students[Social_Comparison_Frequency],
    "Never", 1,
    "Rarely", 2,
    "Sometimes", 3,
    "Frequently", 4,
    "Always", 5
)

### Column 6: Impact Sort

Impact Sort =
SWITCH(
    Students[Overall_Impact],
    "Beneficial", 1,
    "Neutral", 2,
    "Negative", 3
)


### Measures

Total Students = COUNTROWS(Students)

Avg Daily Usage = AVERAGE(Students[Daily_Usage_Hours])

Avg GPA = AVERAGE(Students[Academic_Performance_GPA])

Avg Mental Health = AVERAGE(Students[Mental_Health_Index])

Avg Sleep = AVERAGE(Students[Sleep_Duration_Hours])

Avg Stress = AVERAGE(Students[Perceived_Stress_Score])

% Negative Impact =
DIVIDE(
    CALCULATE(COUNTROWS(Students), Students[Overall_Impact] = "Negative"),
    COUNTROWS(Students)
% Late Night Users =
DIVIDE(
    CALCULATE(COUNTROWS(Students), Students[Late Night Use] = "Yes"),
    COUNTROWS(Students)
)
 ## Visualization
 
### Page 1, Overview

#### Five KPI cards
Card 1: Total Students
Card 2: Avg Daily Usage
Card 3: Avg GPA
Card 4: Avg Mental Health
Card 5: % Negative Impact

#### Donut chart: Overall Impact  (Title: Overall Impact of Social Media)
Drag Overall_Impact into Legend.
Drag Total Students into Values.

#### Bar chart: Platforms(Title: Students by Primary Platform)
Clustered bar chart icon.
Primary_Platform into Y-axis and Total Students into X-axis

#### Column chart: Usage by academic level(Average Daily Usage by Academic Level)

#### Clustered column chart icon.
Academic_Level into X-axis and Avg Daily Usage into Y-axis.

#### Add four slicers, each from the Slicer icon
##### Gender
##### Academic_Level
##### Device_Type
##### Age Group

### Page 2, Usage vs. Wellbeing

##### Scatter: Usage vs Mental Health (Title: More daily use is linked to lower mental health)
Click the Scatter chart icon.
X-axis: Daily_Usage_Hours. Y-axis: Mental_Health_Index

##### Combo chart: Usage band vs GPA and Mental Health(Title: GPA and Mental Health by Usage Level)
Click the Line and clustered column chart icon.
X-axis: Usage Band.
Column y-axis: Avg GPA.
Line y-axis: Avg Mental Health

##### Stress by sleep(Stress Falls as Sleep Increases)
Click the Clustered column chart icon.
X-axis: Sleep Band. Y-axis: Avg Stress

##### Social comparison line chart(Mental Health by Social Comparison Frequency)
Click the Line chart icon.
X-axis: Social_Comparison_Frequency
Y-axis: Avg Mental Health

##### Late-night usage
Click the Clustered column chart icon.
X-axis: Late Night Use.
Y-axis: drag in Avg Sleep and Avg GPA

##### Decomposition tree
Click the Decomposition tree icon.
Analyze: Avg Mental Health.
Explain by: Usage Band, Sleep Band, Late Night Use, Primary_Platform

### Page 3, Student Segments

##### matrix(Mental Health: Platform × Usage Level)
Click the Matrix icon.
Rows: Primary_Platform. Columns: Usage Band. Values: Avg Mental Health

##### stacked bar: Impact by usage band (Share of Negative Impact Grows with Usage)
Click the stacked bar chart icon.
Y-axis: Usage Band. X-axis: Total Students. Legend: Overall_Impact

##### Gender comparison(Usage and Mental Health by Gender)
Click the Clustered bar chart icon.
Y-axis: Gender. X-axis: Avg Daily Usage and Avg Mental Health

##### Heavy-user table (Top 10 Heaviest Users)
Click the Table icon.
Add Student_ID, Age, Primary_Platform, Daily_Usage_Hours, Mental_Health_Index, Academic_Performance_GPA, Overall_Impact

##### Sync the slicers across pages
Click View → Sync slicers
For each page, tick both the Sync and Visible

