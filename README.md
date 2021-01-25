# School_District_Analysis
## Project Overview
Assist chief data scientist of a city school district in analyzing student funding and student standardized test data to provide insight on trends in school performance to assist school board in making decisions regarding school budget. 

This analysis will be done by examining the following metrics:

   * Top 5 and bottom 5 performing schools based on the overall passing rate
   * Average math score received by students in each grade level at each school
   * Average reading score received by students in each grade level at each school
   * School performance based on budget per student
   * School performance based on school size
   * School performance based on school type

## Resources
Data source: schools_complete.csv, students_complete.csv

Software: Anaconda 4.9.2, Jupyter Notebook, Python 3.7.9

## Initial Data Read
Once the data files were loaded and stored in a Dataframe, I had to clean the student name data by removing unnecessary prefixes and suffixes, such as "Dr", "Ms.", "PhD" etc., from the list of names. This had to be done so the student scores would coincide with school records. Family related suffixes such as "Jr.", "II", "III", etc. were left attached. This was done by first declaring a list of each prefix and suffix to be removed (**prefixes_suffixes**). Next, the list was iterated through using a for loop and to replace each item in the list, the **replace()** method was used on the student_name column. The code looked as follows:
        
    for word in prefixes_suffixes:
        student_data_df["student_name"]=  student_data_df["student_name"].str.replace(word,"")
This replaced the prefixes and suffixes with a blank space. Now, the analysis could begin.

## Results
### District Summary

Looking at the below screenshot, we can see that there is a total of 15 schools in this district housing 39,170 total students. The average math and reading scores of students were above the passing grade (>=70) at 79 and 81.9 respectively. The percent of total students that passed math and reading respectively were 75% and 86%. However, the percentage of the student population that passed both math and reading dropped to 65%.

<img width="472" alt="Original_District_Results" src="https://user-images.githubusercontent.com/74752756/105659449-62bf4000-5e8e-11eb-9c81-2d9b28785f33.PNG">

### School Type
Examining the schools by type, we see that Charter schools perfomed better in both math and reading. The screenshot below shows the average math score amongst charter school students is 83.5 and reading is 83.9 compared to district students with an average math score of 77.0 and reading of 81.0. The percentage of Charter students that passed both reading and math is 90% versus on 54% of District students passing both subjects.

<img width="369" alt="Original_by_Type" src="https://user-images.githubusercontent.com/74752756/105659493-78346a00-5e8e-11eb-8270-dd3441f5ca6a.PNG">

The top 5 performing schools were all charter schools and conversely the bottom 5 performing schools were all district schools, as illustrated by the below snapshots. 

<img width="504" alt="Original_Top_5" src="https://user-images.githubusercontent.com/74752756/105659530-8da99400-5e8e-11eb-9c10-61c1627ebd4d.PNG">

<img width="502" alt="Original_Bottom_5" src="https://user-images.githubusercontent.com/74752756/105659567-9e5a0a00-5e8e-11eb-9d53-4d2f8be148c1.PNG">

### Replacing Ninth-Grade Scores

It was then requested the reading and math scores of 9th graders at Thomas High School be replaced with NaN, which was done using the loc method as shown below:

    student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th") , ["reading_score"]] = np.nan

    student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th") , ["math_score"]] = np.nan

Interstingly, the removal of these students' scores did not grossly affect the overall data. 

Prior to replacing the 9th graders scores at Thomas High School (THS), the percentage of THS students who passed math, reading, and both subjects was 93.3%, 97.3%, and 90.9%, respectively. When the 9th grade scores were replaced there was a slight drop (0.2%-0.3%) in these percentages, 93.1% in math, 97.0% in reading, and 90.6% in both subjects. Even with the score replacement, there was very minimal impact on THS overall perfomance, as it remained in the top 2 schools. The image below shows the top 5 performing schools after the data replacement. 

<img width="499" alt="Adjusted_Top_5" src="https://user-images.githubusercontent.com/74752756/105659578-aa45cc00-5e8e-11eb-8f26-80c34c0768fd.PNG">

#### Scores by Grade
The replacemet of the 9th grade scores obviously only impacted the math and reading scores of the THS 9th graders. Before the replacement, average math and reading scores for THS 9th graders were 83.59 and 83.73 respectively. After the replacement, NaN was recorded for scores of the ninth-grade students at THS. 

#### Scores by School Spending
The replacement of the 9th grade scores had no impact on the average spending per student in THS. It remained at $638. This remained unaffected becuase the size (number of students) of THS remained the same. 

#### Scores by Size
The substitution of the 9th grade scores had no impact on the size of the schools or on their respective scores. Despite the substituion, THS remained a medium type school in the 1000-2000 size bracket. The average math score, average reading score, percent passing math, percent passing reading, percent passing both all reamined the same after the adjustment.

Original:

<img width="387" alt="Original_by_Size" src="https://user-images.githubusercontent.com/74752756/105660444-a31fbd80-5e90-11eb-920b-8f0a39437922.PNG">

Adjusted:

<img width="385" alt="Adjusted_by_Size" src="https://user-images.githubusercontent.com/74752756/105660588-f5f97500-5e90-11eb-84f9-8524fd8d7c29.PNG">


#### Scores by School Type
The change of the 9th grader data had no impact on scores by school type. The average math and reading scorese were the same before and after the change, as seen in the images below

Adjusted data:

<img width="362" alt="Adjusted_by_Type" src="https://user-images.githubusercontent.com/74752756/105659595-b893e800-5e8e-11eb-8c05-b984860f0ac5.PNG">

Original data:

<img width="369" alt="Original_by_Type" src="https://user-images.githubusercontent.com/74752756/105659493-78346a00-5e8e-11eb-8270-dd3441f5ca6a.PNG">


## Summary
Overall, the removal of the 9th grade results at Thomas High School had no major affects on the original findings.
  1. *Percentage of Students passing math at THS*- There was a 0.2% decrease in the percentage of students who passed math at Thomas high school. Prior to the data adjustment,   93.3% of students passed math. This percentage only dropped down to 93.1% after.
  
  2. *Percentage of Students passing reading at THS*- The percentage of THS students passing reading was 97.3% prior to the removal of the 9th graders scores. After, the figure dropped to 97.0%, which is still a very high passing perentage. 
  
  3.*Percentage of Students passing both math and reading*- Prior to the adjustment of the 9the graders scores, the percntage of THS students who passeed both math and reading was 90.9%. This dipped to 90.6% after the adjustment.
  
  4. *Math and reading scores by grade*- Prior to the removal of the dadta, 9th graders at Thomas High School had an average math score of 83.59 and an average reading score of 83.73. There was no score recorded for 9th grade students at THS after the adjustment. 
