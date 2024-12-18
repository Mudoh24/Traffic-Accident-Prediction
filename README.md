# Traffic-Accident-Prediction Analysis

### Table of Contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results and Findings](#results-and-findings)
- [Recommendations](#recommendations)
- [Data source](#data-source)
  



### Project Overview

![Traffic dashboad](https://github.com/user-attachments/assets/e7436f5c-ae0f-43fc-aca7-476e0d64fdc5)


The accident trends dataset provides insightful information on factors influencing road accidents, encompassing variables like Road Type, Time of Day, Traffic Density, Speed Limit, and Road Conditions. It categorizes accidents by severity, considering attributes such as Driver Age, Driver Experience, Alcohol Consumption, and Vehicle Type.

Analysis of this dataset can reveal patterns in accident occurrence, identifying high-risk road types and conditions (e.g., icy or wet roads) and critical time periods when accidents are most frequent. Insights into the relationship between speed limits, traffic density, and accident severity are crucial for enhancing road safety measures. Furthermore, the dataset enables understanding of demographic and behavioral influences, such as the impact of driver age or experience on accident likelihood.

Key metrics include accident frequency by road condition, severity distribution across vehicle types, and the effect of external factors like light conditions. These trends can inform data-driven policies to mitigate accidents, optimize traffic management, and improve infrastructure safety.

### Data Source
The primary data source used for this analys is the "dataset_traffic_accident_prediction.csv" file that contains various information about various factors of both human and physical that causes influence car accident.

### Tools
- Excel Data Cleaning
- SQL Server Data Analysis
- Power BI - Data report and Visualisation

### Data Cleaning and Preparation
The following tasks were performed;
1. Data loading and insppection
2. Handling of Missing data
3. Data Cleaning and formatting

### Exploratory Data Analysis
The EDA here involves exploring different factors of car accident causes such as;
- which is the overall most caused of car accident?
- What is the peak car accident period?

### Data Analysis
-1. Accident Frequency by Road Type
```SQL
select Road_Type, 
	count(Accident) as total_accident
from traffic_accident
WHERE
 Road_Type IS NOT NULL AND Accident IS NOT NULL
Group by Road_Type;
```

-- 2. Impact of Traffic Density on Accidents
```SQL
select Traffic_Density,
count(Accident) as Accident_per_Density
from traffic_accident
WHERE
 Traffic_Density IS NOT NULL AND Accident IS NOT NULL
group by Traffic_Density;
```
-3. Driver Age and Experience Analysis
  ```SQL
  select Driver_Age,
	    Driver_Experience,
		       CASE
						WHEN Driver_Age between 18 and 25 then '18-25'
						WHEN Driver_Age between 26 and 35 then '26-35'
						WHEN Driver_Age BETWEEN 36 AND 45 THEN '36-45'
						WHEN Driver_Age BETWEEN 46 AND 55 THEN '46-55'
						WHEN Driver_Age > 55 THEN '56+'
						ELSE 'Unknown'
					END AS Age_Range,
    COUNT(*) AS Total_Records,
	Sum(CASE WHEN Accident = 1 then 1 else 0 end) as Total_Accidents,
	ROUND((SUM(CASE WHEN Accident = 1 then 1 else 0 end)*100 / COUNT(*)),2) as Accident_rate

from traffic_accident

where Driver_Experience is not null and Driver_Age is not null

GROUP BY 
		CASE
						WHEN Driver_Age BETWEEN 18 AND 25 then '18-25'
						WHEN Driver_Age BETWEEN 26 AND 35 then '26-35'
						WHEN Driver_Age BETWEEN 36 AND 45 THEN '36-45'
						WHEN Driver_Age BETWEEN 46 AND 55 THEN '46-55'
						WHEN Driver_Age > 55 THEN '56+'
						ELSE 'Unknown'
					END,
		 Driver_Age,
		 Driver_Experience
ORDER BY 
		Total_Accidents desc;
  ```
- 4. Accident Severity by Road Condition
```SQL
SELECT Road_Condition,
		Accident_Severity,
		count(Accident) as Total_accidents
from traffic_accident
WHERE
 Accident_Severity IS NOT NULL AND Road_Condition IS NOT NULL
Group by Road_Condition,
		Accident_Severity
Order by Accident_Severity desc;
```
- 5. Time of Day vs. Accident Rates
```SQL
SELECT Time_of_Day,
	   Count(Accident) As Total_accident
from traffic_accident
where Time_of_Day IS NOT NULL AND Accident IS NOT NULL
Group by Time_of_Day
order by Total_accident desc;
```
- 6. Vehicle Type Contribution to Accidents
```SQL
Select Vehicle_Type,
Count(Accident) As Total_Accidents
from traffic_accident
where Vehicle_Type is not null and Accident is not null
group by Vehicle_Type
order by Total_Accidents desc;
```
- 7. Road Light Condition Impact
```SQL
SELECT Road_Light_Condition,
		count(Accident) as Total_Accidents
from traffic_accident
where Road_Light_Condition is not null and Accident is not null
group by Road_Light_Condition
order by Total_Accidents desc;
```

### Results and Findings
The traffic accident analysis dashboard provides a detailed breakdown of accident trends, contributing factors, and areas for improvement. Key highlights include:

- Accident by Age-Range: Drivers aged 56+ account for the highest accidents (62), while those aged 18-25 have the lowest (23).
- Accident by Road Light: Most accidents occur under Artificial Light, followed by Daylight and fewer in No Light conditions.
- Accidents by Time of Day: Accidents are most frequent in the Afternoon (above 250), with a decline in Evening, Morning, and Night.
- Accident by Vehicle Type: Cars are the most involved vehicle type in accidents, while trucks, motorcycles, and buses show significantly lower occurrences.
- Accident by Traffic Density: Medium Density traffic (241) has the highest accident share (31.17%), with Low and High Density contributing 30.53% and 37.77%, respectively.
- Accident by Road Condition: Most accidents occur on Dry roads, with fewer on Icy, Wet, or Under Construction roads.
- Accidents by Road Type: City Roads experience the most accidents (216, 31.56%), followed by Highways and Rural Roads.
Overall, the analysis highlights that artificial light, medium traffic density, city roads, and afternoon periods are key contributing factors to accidents. This data emphasizes the need for targeted safety measures.

### Recommendations
Based on the analysis, the following recommendations can help reduce traffic accidents:

Improve Road Safety in City Areas: Since city roads have the highest accident rates, implement stricter speed limits, better signage, and enhanced road infrastructure.
- Enhanced Visibility: Most accidents occur under artificial light, suggesting the need for improved street lighting and reflective road markers to enhance visibility at night.
- Target Afternoon Hours: Increase traffic enforcement and awareness campaigns during the afternoon, when accidents peak, to encourage safe driving practices.
- Traffic Management: Address medium traffic density areas with better flow management, signal optimization, and congestion monitoring.
- Driver Education: Focus on drivers aged 56+ and new drivers, offering refresher training and awareness on defensive driving techniques.
- Road Condition Maintenance: Regularly maintain icy and wet roads to minimize risks, particularly in adverse weather conditions.
Implementing these targeted measures can significantly reduce accident rates and improve road safety.

### Data source
[dataset_traffic_accident_prediction](https://www.kaggle.com/datasets/denkuznetz/traffic-accident-prediction?select=dataset_traffic_accident_prediction1.csv)
