# US Accidents (2016-2023)

## Overview
#### Traffic Accidents represent a significant  challenge affecting millions of people across the U.S. each year. With the continuous increase in vehicle numbers and expansion of the road network, accidents necessitate research to identify the contributing factors to the rising number of injuries and fatalities. Despite advancements in transportation systems, safety technologies, and the efforts of traffic authorities and specialized agencies, national accident trends indicate a persistent rise in crash rates across many regions.
This project analyzes U.S. traffic accidents from 2016 to 2023 with the objective of identifying the conditions that contribute to higher crash severity. By examining the interaction between time patterns, weather conditions, visibility(mi), distance(mi), and road type, this study provides a comprehensive, data-driven assessment that can inform the development of more effective road-safety policies aimed at reducing accident occurrence and severity.

## Dataset Description:

#### 1. Data Source: Traffic streaming APIs that broadcast live events

#### 2. Data Link: https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents

#### 3. Time Period: 2016-2023

#### 4. Rows: 7.7M

#### 5. Columns: 46

## Data Cleaning & Preparation 

#### 1) Check Null Values

##### 1.1 Null in City

<img width="1104" height="518" alt="Screenshot 2025-11-25 at 8 42 34 PM" src="https://github.com/user-attachments/assets/e4d66832-c098-4a82-8012-62362311eba0" />


###### Fill missing City by using the most common (mode) city for the same State
def fill_city_by_state(row):
    if pd.isna(row["City"]):
        state = row["State"]
        mode_city = Accidents[Accidents["State"] == state]["City"].mode()
        return mode_city.iloc[0] if len(mode_city)>0 else "Unknown"
    return row["City"]

Accidents["City"] = Accidents.apply(fill_city_by_state, axis=1)

##### 1.2 Null in Weather Condition & Daytime

<img width="1171" height="352" alt="Screenshot 2025-11-25 at 8 44 28 PM" src="https://github.com/user-attachments/assets/f881f5f4-3a11-4acd-a587-334b02eb8986" />


#### 2) Check Duplicates

0 Duplicates

#### 3) Change Data Type

##### Filter rows where Start_Time contains '.000'
Accidents[Accidents['Start_Time'].str.contains('.000')]

##### Filter rows where End_Time contains '.000'
Accidents[Accidents['End_Time'].str.contains('.000')]

##### Clean Start_Time  & ِEnd_time by removing (.) in  fractional seconds 
Accidents["Start_Time"] = Accidents["Start_Time"].astype(str).str.split('.').str[0]
Accidents["End_Time"]   = Accidents["End_Time"].astype(str).str.split('.').str[0]

##### Convert Start_Time & End_Time to a datetime object
Accidents['Start_Time'] = pd.to_datetime (Accidents['Start_Time'])
Accidents['End_Time'] = pd.to_datetime (Accidents['End_Time'])

#### 4) Categorize Weather Conditions
('Rain', 'Cloudy', 'Snow', 'Fog', 'Clear', 'Ice & Freezing',
       'Hazard', 'Thunderstorm')

## Key Insight

#### 1. Accident risk has increased every year.

#### 2. California has the most accidents.

#### 3. Monday and weekdays show highest accidents.

#### 4. Seasons don’t affect severity.

#### 5. Severe accidents peak at 7–9 AM and 4–6 PM.

#### 56 Rain and fog increase accident risk.

#### 7. Low visibility causes higher severity.

#### 8. Rain causes most severe accidents.

#### 9. Humidity doesn’t impact severity.

#### 10. Crossings and signals have the most crashes.

#### 11. At night, junctions and railways are most severe.

#### 12. Short/long distance = higher severity







## Recommendations

#### 1. Improve Infrastructure in High-Risk Areas

#### 2. Launch Awareness Campaigns About Road Safety

#### 3. Manage Traffic During Rush Hours

#### 4. Send Alerts During Hazardous Weather Conditions

#### 5. Improve Nighttime Road Lighting

#### 6. Promote Safe Driving Behavior


## Tools & Libraries
#### 1. Python: Pandas
#### 2. Tableau: Visulizations 
