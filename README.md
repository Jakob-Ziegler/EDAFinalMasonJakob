# EDAFinalMasonJakob
Contains all R code for the final project in EDA. 
#import all necessary libraries
```{r libraries}
library(readr)
library(dplyr)
library(ggplot2)
library(plotly)

```


#this block is used to read in the data
```{r data}
gym_members_exercise_tracking <- read_csv("gym_members_exercise_tracking.csv")
```

#this block is used to make all necessary conversions for the data
```{r pre-processing}
#creates a new data frame that all further manipulations will be perfomed on
gym = gym_members_exercise_tracking

#converts the weight into pounds from kilograms 
#renames it to "Weight (lbs)"
gym = gym %>%
  mutate(`Weight (kg)` = round(`Weight (kg)` * 2.20462, 1))
gym = gym %>%
  rename(`Weight (lbs)` = `Weight (kg)`)

#converts the height into inches from meters 
#renames it to "Height (in)"
gym = gym %>% 
  mutate(`Height (m)` = round(`Height (m)` * 39.3701, 1))
gym = gym %>%
  rename(`Height (in)` = `Height (m)`)

#converts the gym session duration from hours to minutes
#renames it to "Session_Duration (mins)"
gym = gym %>%
  mutate(`Session_Duration (hours)` = round(`Session_Duration (hours)` * 60, 2))
gym = gym %>%
  rename(`Session_Duration (mins)` = `Session_Duration (hours)`)

#Converts water intake from liters to ounces
#renames it to "Water_Intake (Ounces)"
gym = gym %>%
  mutate(`Water_Intake (liters)` = round(`Water_Intake (liters)` * 33.814, 1))
gym = gym %>%
  rename(`Water_Intake (ounces)` = `Water_Intake (liters)`)

#adds 4 different age groups 
gym = gym %>%
  mutate(Group = case_when(
    Age >= 18 & Age <= 29 ~ "18-29",
    Age >= 30 & Age <= 39 ~ "30-39",
    Age >= 40 & Age <= 49 ~ "40-49",
    Age >= 50 & Age <= 59 ~ "50-59"
  ))

#adds 4 different weight groups 
gym = gym %>%
  mutate(Group_WGT = case_when(
    `Weight (lbs)` >= 88 & `Weight (lbs)` <= 138 ~ "88 - 138",
    `Weight (lbs)` >= 138.01 & `Weight (lbs)` <= 188 ~ "138 - 188",
    `Weight (lbs)` >= 188.01 & `Weight (lbs)` <= 238 ~ "188 - 238",
    `Weight (lbs)` >= 238.01 & `Weight (lbs)` <= 288 ~ "238 - 288"
  ))

```

