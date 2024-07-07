# BellaBeat
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
         The public dataset  Fitbit Fitness Tracker Data is made available by Mobius contains personal fitness tracker data which includes heart rate, minute-level output for physical activity and sleep monitoring. Information about the daily activity, steps and heart rate can be used to explore user’s habits. See data https://www.kaggle.com/datasets/arashnic/fitbit?resource=download 
*The dataset is either a wide or long dataset that is stored in 18 CSV files, but i focused my analysis on the following:*
+ dailyActivity_merged
+ dailyCalories_merged
+ dailySteps_merged
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
####What tools are you choosing and why?
I will be using three tools for this project, which are; Google Sheets, SQL and Tableau. For this stage we will be using Google Sheets for the cleaning process, SQL for the analyzing process and Tableau for visualization.

For the cleaning process i used Excel to remove duplicates, to change format and to verify unique values.