# README: Cyclist Casualties Gender Analysis
## Project Overview
This repository contains the analysis of gender differences in cyclist casualties and injury risks in England, using secondary data from the **STATS19 dataset** (which records personal injury accidents on public roads) and the **National Travel Survey (NTS)** for the year 2019. The study investigates whether gender has a statistical impact on the likelihood of being involved in a cycling accident, suffering a fatal or serious injury (KSI), and the relationship between cycling frequency or duration and injury risks.

The analysis was conducted using **SPSS** for statistical testing and **Excel** for the final risk calculation.


# Table of Contents

1. [Introduction](#introduction)
2. [Objectives](#objectives)
3. [Research Hypotheses](#research-hypotheses)
4. [Data Sources](#data-sources)
5. [Tools Used](#tools-used)
6. [Data Preprocessing](#data-preprocessing)
7. [Data Analysis Methodology](#data-analysis-methodology)
8. [Findings](#findings)
9. [Discussion](#discussion)
10. [References](#references)



## Introduction
Cycling holds great potential as a sustainable mode of transportation, offering numerous health and environmental benefits. However, safety concerns remain a significant barrier to its broader adoption. Cyclists are disproportionately affected by road accidents, especially in fatal and serious injury cases. This study focuses on examining the gender differences in cyclist injury risks to determine if men and women face different odds of being involved in severe cycling accidents. By analyzing cycling habits and exposure data, the study aims to uncover whether these differences are due to varying cycling behaviors or other underlying factors.


## Objectives
1. Understand the gender differences in cycling accident rates.
2. Assess if men are more prone to fatal or severe injuries (KSI) compared to women.
3. Analyze whether men tend to cycle longer distances and durations than women, contributing to the higher exposure risk


## Research Hypotheses
1.	Cycling Crash Likelihood by Gender: Men are more likely to be involved in cycling crashes compared to women.
2.	KSI Risk by Gender: Male cyclists face a higher risk of suffering a KSI (killed or seriously injured) compared to female cyclists.
3.	Cycling Exposure by Gender: Men cycle longer distances and durations compared to women, which may explain the differences in injury rates.


## Data Sources
1. STATS19 Road Safety Data (2019): Includes accident and casualty data for personal injury accidents on public roads in the UK. Key datasets include:

- Dft_Road_Safety_Accident: Each row represents a collision.
- Dft_Road_Safety_Casualty: Contains multiple rows per accident index.

**See Variable Lookup data for Road safety data variable and guide** and Department for Transport’s for [quality data report](https://www.gov.uk/government/publications/reported-road-casualty-statistics-background-quality-report).

2. National Travel Survey (NTS 2019): An annual household survey tracking travel behavior in England, used to calculate cycling exposure by gender.
Datasets: Trip_eul2002-2019 and Individual_2002-2019


## Tools Used
- **SPSS**: For statistical testing and analysis.
- **Excel**: For final risk calculations and data normalization.

# Data Preprocessing
1.	Road Safety Data:
- 	 **Merging Datasets**: The Accident and Casualties datasets were merged using a one-to-many relationship, ensuring that each accident record could link to multiple casualty records.
- **Filtering**: The data was filtered to include only incidents that occurred in England, aligning with the National Travel Survey (NTS) data scope, which covers England exclusively.
- **Focusing on Cyclists**:
  - The `Casualty_Type` variable was recoded to create a new binary variable: **“Casualty is a cyclist.”**
    - `0` = Non-cyclists
    - `1` = Cyclists
- **KSI Variable Creation**:
  - A new KSI (Killed or Seriously Injured) variable was derived from the `Casualty_Severity` field, with killed and seriously injured cases recoded as 1 (severe) and slightly injured as 0 (non-severe). (See Fig. 1 below for SQL syntax.)


![image](https://github.com/user-attachments/assets/ba10503e-2724-4758-bbbf-bdcfc9f47b57)

2.	NTS Datasets: The Trip_eul2002-2019 and Individual_2002-2019 datasets were reorganized and limited to the year 2019.

From the Trip_eul_2019 data:
**Cycling Trips Extraction**: Journeys made by cyclists were extracted, creating a new dataset called Cycling_Trips, which includes:
Number of cycling trips
Time spent (in minutes)
Distance traveled (in miles)

- **Merging with Individual Data**: The Individual_eul_2019 dataset provided information on respondent gender, which was merged with the Cycling_Trips dataset to link cycling activity with gender.

- **Data Cleaning** The final dataset (see Figure 1) was refined by removing missing values, specifically for individuals who did not cycle during the survey week or who failed to complete their travel diaries

![image](https://github.com/user-attachments/assets/18127653-b2da-470c-8b10-829bfac34b09)


## Data Analysis Methodology

### Chi- Square Test

Given the categorical nature of data, Chi-square tests were conducted to assess the association between gender and the likelihood of:
•	Being involved in a cycling accident
•	Suffering a fatal or serious injury (KSI)

1.	**Null Hypothesis (H₀₁):** There is no significant difference in the likelihood of being involved in a cycling accident between men and women.

   ![image](https://github.com/user-attachments/assets/ea94fd2c-a353-46fb-b1bf-819c4057c7f7)

   ![image](https://github.com/user-attachments/assets/1b7f21df-9860-43b0-be24-03cd7704462a)

- Out of 15,849 cyclist casualties, 80.1% were male and 19.9% were female. The Pearson Chi-Square test (X² = 2972.624, p < 0.001) indicated a statistically significant relationship between gender and accident involvement, rejecting the null hypothesis (H₀₁). This suggest that 
 male cyclists are significantly more likely to be involved in accidents than female cyclists and that there is a significant association between gender and involvement in cycling accidents.


2. **Null Hypothesis H₀₂:** There is no significant difference in the risk of suffering a fatal or serious injury (KSI) between male and female cyclists.

To test Hypothesis 2, cases were temporary filtered to include KSI only (Fig 2.) and cross-tabulation was performed to examine the relationship between Cyclist status - Sex of casualty.

![image](https://github.com/user-attachments/assets/1c5af360-a1ad-437f-96c8-4496c33e8c45)

![image](https://github.com/user-attachments/assets/3b73414e-e571-4022-9484-368f65b4ba71)

![image](https://github.com/user-attachments/assets/0dc5d74e-afee-43af-804c-ed2b7259b9bf)


For KSI casualties, males were significantly overrepresented with  The Pearson Chi-Square test (X² = 291.519, p < 0.001) confirmed that gender and KSI involvement are dependent, leading to the rejection of the null hypothesis (H₀₂). Men face a disproportionately higher risk of fatal or severe injuries in cycling accidents

### Cyclist Injury Risk by Gender for million population
Next in Excel, we normalized cyclist casualty and KSI data using the Mid-2019 Population Estimates from the ONS, calculating risk rates per million population. Gender differences were accounted for by adjusting rates to reflect population size, mitigating biases from unequal exposure. This provided a clearer comparison of injury risks across demographic groups. 

### 
