[bquxjob_2a277a7f_190cc4b688b (1).csv](https://github.com/user-attachments/files/16316062/bquxjob_2a277a7f_190cc4b688b.1.csv)[bquxjob_454df10e_190c3601c1c.csv](https://github.com/user-attachments/files/16276352/bquxjob_454df10e_190c3601c1c.csv)# BellaBeat
## How Can A Wellness Technology Play It Smart

### ASK
#### What is the problem you are trying to solve? 
I am a junior data analyst working on the marketing analyst team at Bellabeat and will want to understand how other smart device users use Bellabeat devices to monitor and improve 
 their health and wellness to help them unlock new growth opportunities for the  company.

#### How can your insights drive business decisions?
I will be finding relevant patterns and trends in whatever information found in the leaf smart device and how the smart device is being utilized.

#### Key Stakeholders:
+ Chief Creative Officer and Bellabeat’s Co-founder.(Urska Srsen)
+ Bellabeat Executive Team: Sando Mur (Mathematician and Bellabeat Co-founder)
+ Bellabeat’s marketing analytics team

#### Business Task
To focus on one Bellabeat’s product and analyze the smart device data  to gain insight into how customers are using their smart device. The insight will help in guiding marketing strategy for the company and enable presentation to the stakeholders along with high-level recommendations for the company’s marketing strategy.

### PREPARE
The public dataset  Fitbit Fitness Tracker Data is made available by Mobius contains personal fitness tracker data which includes heart rate, minute-level output for physical activity and sleep monitoring. Information about the daily activity, steps and heart rate can be used to explore user’s habits. 
See data https://www.kaggle.com/datasets/arashnic/fitbit?resource=download 

*The dataset is either a wide or long dataset that is stored in 18 CSV files, but i focused my analysis on the following:*
+ dailyActivity_merged
+ sleepDay_merged
+ weightLoginfo_merged

#### Data limitations
The dataset was collected from 30 FitBit users which is a small population and does not represent the entire fitness population. The data was collected six years ago which renders the insights derived from the data irrelevant and untimely because there could be a change in user fitness, sleeping habits, diet, food consumption and daily activity.

#### Data credibility
Let’s follow the ROCCC criteria
Reliability: The data contains fitness data relating to sleep,step taken, heart rate and calorie intake.
Original: The data is third party data collected using Amazon Mechanical Turk. Therefore, the originality is low.
Comprehensive: Missing information on the age,gender,device type used on the tracking etc. hence, it is not comprehensive.
Current: These datasets were genderated by respondents to a distributed survey in 2016 via Amazon Mechanical Turk.
Cited: the dataset is properly cited because it is considered as crowdsourcing data generated by respondent to a distributed survey.

### PROCESS
#### What tools are you choosing and why?
I will be using three tools for this project, which are; Google Sheets, SQL and Tableau. For this stage we will be using Google Sheets for the cleaning process, SQL for the analyzing process and Tableau for visualization.

For the cleaning process i used Google Sheets to remove duplicates, remove blanks using conditional formatting, to change format and to verify unique values for all tables.
1.  For the *dailyActivity_merged table* the column name 'activitydate' was changed to 'Date'
   + The coiumn names 'TrackerDistance', 'LoggedDistance', and 'SedentaryActiveDistance' were removed.
   + The table was renamed *'DailyActivity_Merged_Cleaned'*

2.  For the *sleepDay_merged* table the column name 'sleepday' was changed to 'Date'.
   + The 'SleepDay' column was changed into two separate columns 'Date' and 'Time'.
   + A new column 'Time_Awake' was created by subtracting column 'TotalMinutes_Asleep' from column 'TotalTime_In_Bed'.
   + The column 'Total Sleep Records' was removed.
   + The table was renamed as *'SleepDay_Merged_Cleaned'*

3.  For the *weightLoginfo_merged*  the column 'Manual Report' was changed to 'Report_Type'.
   + Removed columns 'Fat' and 'LogId'
   + The table was renamed *'WeightLogInfo_Merged_Cleaned'*

### ANALYZE AND SHARE

After the data was cleaned using Google Spreadsheet, I will bwe using SQL to continue my analysis
The cleaned data was downloaded and moved to SQL by:
  + Creating a dataset of each data then creating a table of each data
  + Observing the schema of each data and preview each data before querying the data.

#### Checking the number of unique ids in each dataset
    SELECT COUNT(DISTINCT id) AS unique_id 
    FROM `my-sandbox-project-417117.dailyactivities_data.dailyactivities`

This query was repeated for all the tables substituting the correct table names in each case, The results are as follows:
   + *DailyActivities_Merged_Cleaned - 33 unique ids/users*
   + *SleepDay_merged_Cleaned - 24 unique ids/users*
   + *WeightLogInfo_merged_Cleaned - 8 unique ids/users*

The initial objective was to determine the frequency with which each user ID appeared in the logs, essentially measuring how often each users were using their Fitbit smart devices. The 
 query below shows how this can be achieved.
     
     SELECT id,
     COUNT(id) AS total_id
     FROM `my-sandbox-project-417117.dailyactivities_data.dailyactivities`
     GROUP BY id

 *This shows that the dailyactivity for each user id ranged from 4 to 31 times.*

 Now i classified their activities into three classes, which are; Active users, Moderate users and Light users.

      SELECT id,
      COUNT(id) AS total_uses,
      CASE
      WHEN COUNT(id) BETWEEN 21 AND 31 THEN 'active_user'
      WHEN COUNT(id) BETWEEN 11 and 20 THEN 'moderate_user'
      WHEN COUNT(id) BETWEEN 0 and 10 THEN 'light_user'
      END AS user_classification
      FROM `my-sandbox-project-417117.dailyactivities_data.dailyactivities`
      GROUP BY id
 
 *The result shows that there are more active users than moderate users or light users*
![Sheet 1](https://github.com/user-attachments/assets/1fd8bc3e-037d-455e-adc2-309ccf79c274)

 We will now compare activities and calories in the dailyactivity_merged_cleaned dataset

      SELECT Id,
      SUM(Steps) as total_steps,
      SUM(VeryActive_Minutes) as total_Vactive_mins,
      SUM(FairlyActive_Minutes)  as total_Factive_mins,
      SUM(LightlyActive_Minutes) as total_Lactive_min,
      SUM(Calories) as total_calories 
      FROM `my-sandbox-project-417117.dailyactivities_data.dailyactivities`
      GROUP BY Id

*This shows there is a stron correlation between calories burned and activity intense time*

Now i analyze the dataset to identify the individuals with the highest average number of minutes spent being actively engaged

     SELECT Id,
     ROUND(AVG(VeryActive_Minutes),2) as avg_Vactive_mins,
     ROUND(AVG(FairlyActive_Minutes),2)  as avg_Factive_mins,
     ROUND(AVG(LightlyActive_Minutes),2) as avg_Lactive_min,
     ROUND(AVG(Sedentary_Minutes),2) as avg_sedantary_mins 
     FROM `my-sandbox-project-417117.dailyactivities_data.dailyactivities`
     GROUP BY Id
     ORDER BY 2,3,4,5 DESC 
     
![Sheet 1 (1)](https://github.com/user-attachments/assets/f48ced52-1c19-4a7e-8a78-3ba9a2f5c8c6)

*This shows that the sedentary minutes was the highest on  average*

The most and least activity days on the average is then identified using this query

    SELECT Weekday,
     ROUND(AVG(VeryActive_Minutes),2) as avg_Vactive_mins,
     ROUND(AVG(FairlyActive_Minutes),2)  as avg_Factive_mins,
     ROUND(AVG(LightlyActive_Minutes),2) as avg_Lactive_min,
     ROUND(AVG(Sedentary_Minutes),2) as avg_sedantary_mins 
    FROM `my-sandbox-project-417117.dailyactivities_data.dailyactiviteis`
    GROUP BY Weekday
    ORDER BY 2,3,4,5 DESC

![avg_Vactive_mins, avg_Factive_mins, avg_Lactive_min, avg_sedantary_mins by Weekday](https://github.com/user-attachments/assets/409455c4-953e-4fa7-9642-e7931c7bbeec)

     SELECT Weekday,
         ROUND(AVG(VeryActive_Minutes + FairlyActive_Minutes + LightlyActive_Minutes),2) as total_avg_active_mins,
         ROUND(AVG(Sedentary_Minutes),2) as avg_sedantary_mins,
         ROUND(AVG(Calories), 2) AS avg_calories
     FROM `my-sandbox-project-417117.dailyactivities_data.dailyactiviteis` 
     GROUP BY Weekday
     ORDER BY 2,3,4 DESC
     
*The analysis shows that Saturdays are found  to be the most active days with 244mins of combined activity(very active,fairly active and lightly active levels) and Sunday the least 
 recorded with 208mins, The burned calories are found to be consistent daily with Sundays and Thursdays exceptions. Monday is found to be the most sedentary day, while Thursday is 
 with the least.*

Next, I identified how much sleep users get on a average by compiling the sleep data into averages by user Ids then convering minutes to hours.

     SELECT id,
     ROUND(AVG(TotalMinutes_Asleep),2) as avg_sleep_time,
     ROUND(AVG(TotalTime_In_Bed),2) as avg_time_bed,
     ROUND(AVG(Time_Awake),2) as avg_time_awake
     FROM `my-sandbox-project-417117.sleep_data.sleep`
     GROUP BY Id

 ![Sheet 1 (2)](https://github.com/user-attachments/assets/d8ed87ca-d08a-424b-a46f-687c3a0a5c60)
       
         SELECT Id,
             ROUND(AVG(TotalTime_In_Bed)/60) AS avg_time_in_bed_h,
             ROUND(AVG(TotalMinutes_Asleep)/60) AS avg_time_asleep_h,
             ROUND(AVG(Time_Awake)/60) AS avg_time_awake_h
         FROM `my-sandbox-project-417117.sleep_data.sleep`
         GROUP BY Id
      
*This result shows that more than 7 users had time disrupted from sleep while in bed and 16 users got atleast 7 hours of sleep and 8 users got less than 7 hours of sleep*

Next, i looked at the average of all activities recorded in the daily activities by using the day of the weeek using this query

      SELECT Weekday,
      ROUND(AVG(Steps),2) AS avg_steps,
      ROUND(AVG(Total_Distance), 2) AS avg_distance,
      ROUND(AVG(Calories), 2) AS avg_calories 
      FROM `my-sandbox-project-417117.dailyactivities_data.dailyactivities`
      GROUP BY Weekday
      ORDER BY 2 DESC

*This results  shows that Saturday registered the highest total steps on average for all the activities recorded.*

![Sheet 1 (3)](https://github.com/user-attachments/assets/761ba14b-aad3-4787-89c3-6baaddaf4b93)

I then combined the daily activity table with the sleep table to look at the relationship using the steps column in the daily activity table

         SELECT sp.id,
             AVG(dailyactivity.Steps) AS avg_totalsteps,
                 dailyactivity.Weekday AS weekday,
             ROUND(AVG(sp.TotalTime_In_Bed)/60) AS avg_time_in_bed_h,
             ROUND(AVG(sp.TotalMinutes_Asleep)/60) AS avg_time_asleep_h,
             ROUND(AVG(sp.Time_Awake)/60) AS avg_time_awake 
         FROM `my-sandbox-project-417117.sleep_data.sleep` AS sp
         INNER JOIN `my-sandbox-project-417117.dailyactivities_data.dailyactiviteis` AS dailyactivity
         ON dailyactivity.Id = sp.Id
         GROUP BY sp.Id,
             dailyactivity.Weekday
         ORDER BY 2 DESC   

*This result shows that on an average users are recording over 9000 steps, the users are found to be meeting the recommended at least 7 hours of sleep*

Next i looked at the time expenditure per day of the daily activities

       SELECT *
       EXCEPT(Weight_Kg,Weight_Pounds,Report_Type),
       CASE WHEN BMI < 18.5 THEN "Underweight"
            WHEN BMI < 25.0 THEN "Healthy"
            WHEN BMI < 30.0 THEN "Overweight"
            ELSE "Obese" END AS BMICategories
       FROM `my-sandbox-project-417117.weightlog_data.weight`
       WHERE BMI > 0
