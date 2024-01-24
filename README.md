# Bellabeat-Case-Study-Project
Bellabeat Case study for Google Data Analytics Capstone Project.
 **Introduction**:
 This case study focuses on tracking and identifying patterns in Fitbit health fitness tracker users to generate a final output for 'Bellabeat'. Bellabeat is a small company that manufactures high-tech products, specifically health-focused smart devices and other wellness products aimed at women worldwide. The objective is to assist the company in achieving its goal of selling smart devices by analyzing patterns and trends among Fitbit users
 
 
 **About the Data and its integrity:**
 * The dataset used for this analysis was obtained from Kaggle, FitBit Fitness Tracker Data. Thirty eligible Fitbit users provided consent for the submission of their personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring and licensed for public domain use.
 
 **Analysis**
 * Project Goal: To identify trends among health smart device users and apply these insights to assist Bellabeat in achieving its company goals. The objective is to recommend strategies for Bellabeat to grow its business and enhance its marketing efforts.
 
 **What I Did**
 * Acquired the dataset with the help of Kaggle, then proceeded to clean and organize the data initially in Excel. For statistical analysis, the dataset was loaded into the R program, performed data manipulation and analysis. Obtained results and created simple visualizations using the R program itself.
 
 **Sharing my statistical analysis(step by step)** 
 * Typical R programming Routine(Installing and loading of R packages)
 
 1. library(tidyverse)
 2. library(lubridate)
 3. library(dplyr)
 4. library(ggplot2)
 5. library(tidyr)
 
 * Installed the datasets manually using Files pane in R by uploading and importing options.
  The datasets I picked are
  
        dailyActivity_mergeddaily_activity_sleep <- merge(daily_activity, daily_sleep, by=c ("Id", "date"))
 
 2. sleepDay_merged
  After reviewing several other datasets, I determined that the datasets mentioned above are sufficient for the specified goal in my opinion.
 
 **CLEANING**
  * I performed cleaning of datasets in the Excel itself and loaded it in the R program then. 
  
 1. From cleanning the datasets we got no duplicates in the dailyActivity dataset and found 3 duplicate rows in sleepDay_merged dataset and removed.
 
 **FORMATTING DATASET**
    
     daily_sleep <- sleepDay_merged
     daily_sleep <- daily_sleep %>%
     mutate(date = as_date(date,format ="%m/%d/%Y %I:%M:%S %p" , tz=Sys.timezone()))
    
 **MERGING DATASET**
 
     daily_activity_sleep <- merge(daily_activity, daily_sleep, by=c ("Id", "date"))
 
 **VISUALIZING THE DATA** 
 
     ggplot(data=daily_activity_sleep, aes(x=TotalMinutesAsleep, y= SedentaryMinutes,)) + geom_point() + geom_smooth() + labs(title = "Sleep time vs Sedementary")
 
  ![f603c4c4-c9d3-4915-a782-ae6a3b0c1dca](https://github.com/newbieyosia/Bellabeat-Case-Study-Project/assets/156952765/41d35645-e1b1-4845-912e-9a38f75508b1)

  **SUMMARIZING DATASET**
 
     summarized_active_time <- daily_activity_sleep %>%
     group_by(Id) %>%
    summarise(avgVeryActiveMinutes = mean(VeryActiveMinutes),
              avgFairlyActiveMinutes = mean(FairlyActiveMinutes),
             avgLightlyActiveMinutes = mean(LightlyActiveMinutes),
             avgSedentaryMinutes = mean(SedentaryMinutes),
             avgMinutesAsleep = mean(TotalMinutesAsleep))
             head(summarized_active_time)

       (Note: Summarizing data to find the activity minutes per day for each individual) 
       
  A tibble: 6 × 6
  
          Id avgVeryActiveMinutes avgFairlyActiveMinutes
          
    <dbl>                     <dbl>                  <dbl>  
       1503960366                37.9                   20.3  
       1644430081                2.5                    19.5  
        1844505072                0                      2.33 
         
          totaltime <- summarized_active_time %>%
          summarise(totalActiveMinutes = mean(avgVeryActiveMinutes),
             totalFairlyActiveMinutes = mean(avgFairlyActiveMinutes),
             totalLightlyActiveMinutes = mean(avgLightlyActiveMinutes),
             totalSedentaryMinutes = mean(avgSedentaryMinutes),
             totalMinutesAsleep = mean(avgMinutesAsleep) ) 
             head(totaltime)

             
      A tibble: 1 × 5
      
      totalActiveMinutes totalFairlyActiveMinutes
      
                <dbl>                    <dbl>
    1               21.8                     15.0
 
        (Note: Summarizing data to find the average active minutes for the individual of a given sample)
                    
     
 **VISUALIZING THE DATA**    
                    
           hours <- c(0.3637242,0.2500249,3.480152,12.98561,6.294125) 
           labls <- c("Active Minutes","Fairly Active Minutes","Lightly Active Minutes","Sedentary Minutes","Total Minutes Asleep")
           pie(hours, labels = labls, density = 300, angle= 60, col =rainbow(5))
     
             
  ![ac460bf8-e648-47b8-85c0-18333bd0c50c](https://github.com/newbieyosia/Bellabeat-Case-Study-Project/assets/156952765/406469da-3f70-42d5-9384-132a5c481b68)

 

 **MY Final Analysis**
 
  So, after all the data cleaning, organizing, manipulating, and visualizing efforts mentioned above, here are my final findings:
 
 1. Well, it's crystal clear from the visuals that people are putting in more time being sedentary, even with less sleep than their sedentary time. Active moments are also quite scarce.
 
  2. So, my suggestion to Bellabeat would be to nudge users when they're stuck in sedentary mode. Motivating them to make the most of their smart health trackers, stay fit, and embrace a healthy lifestyle.
