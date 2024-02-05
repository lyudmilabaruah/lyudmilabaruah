I have used two datasets; for normal queries, I have taken the dataset CHICAGO_CRIME, and for the joins, I have taken the data set COVID-19_ITALY from which the tables I have taken are data_by_region and national_trends.

Q1: To find the total number of crimes in Chicago between 2002 and 2017.
```SQL
SELECT count(*) as total_crimes FROM `bigquery-public-data.chicago_crime.crime` where year between 2002 and 2017;
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/4bb0667b-7fba-4460-be01-bb4854103d35)

Q2: To find the total number of robberies taking place in Chicago.
```SQL
SELECT count(*) as total_robberies FROM `bigquery-public-data.chicago_crime.crime` where primary_type = 'ROBBERY';
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/0b7c6208-db6d-4f4c-bbdb-472f63e7f111)

Q3: To find five dates with the highest number of sidewalk crimes.
 ```SQL
SELECT date, location_description  FROM `bigquery-public-data.chicago_crime.crime` Where location_description = 'SIDEWALK' order by location_description desc Limit 5;
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/16e9b736-9180-4202-b818-9123bb0f379a)

Q4: To find the total number of 'true' arrests.
```
SELECT SUM(CAST(arrest AS INT64)) as total_arrests FROM `bigquery-public-data.chicago_crime.crime` WHERE arrest = TRUE;
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/b355ae52-7cf7-427e-9e59-ed025b9fd612)

Q5: To find the total number of arrests for 'criminal sexual assault.'
```SQL
SELECT SUM(CAST(arrest AS INT64)) as total_arrests FROM `bigquery-public-data.chicago_crime.crime` WHERE primary_type = 'CRIMINAL SEXUAL ASSAULT' AND arrest = true;
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/6ca3b32a-718f-4801-9806-25e968e3bfa9)

Q6: To find the total number of 'false' arrests.
```SQL
SELECT SUM(CASE WHEN arrest = false THEN 1 ELSE 0 END) as total_false_arrests FROM `bigquery-public-data.chicago_crime.crime`;
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/0cab9cd0-bd40-423d-a0a2-f6bee79ff484)

Q7: To find the total number of crimes taking place in 'restaurants.'
```SQL
SELECT COUNT(*) as total_crimes_in_restaurants FROM `bigquery-public-data.chicago_crime.crime` WHERE location_description = 'RESTAURANT';
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/e4fb121f-1731-49fc-af4a-279f91497cb1)

Q8: To find the total number of 'strongarm-no weapon' crimes.
```SQL
SELECT count(*) as total_strongarm_crime  FROM `bigquery-public-data.chicago_crime.crime` where description = 'STRONGARM - NO WEAPON';
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/387955bc-4beb-4ebb-9cdd-e4d197b3d71d)

Q9: To find the total number of 'hospitalized patients' in the 'Piemonte' region and 'Italy' as a whole.
```SQL
SELECT t1.date, t1.total_hospitalized_patients AS national_total, t2.total_hospitalized_patients AS piemonte_total
FROM `bigquery-public-data.covid19_italy.national_trends`t1
LEFT JOIN `bigquery-public-data.covid19_italy.data_by_region`t2 on t1.date = t2.date
AND t1.country = t2.country where t1.country = 'ITA' AND t2.region_name = 'Piemonte';
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/f3e1edd7-2b01-4999-8cbc-10d163dce3d6)

Q10: To find the total number of 'home confinement cases' in the 'Piemonte' region and 'Italy' as a whole.
```SQL
SELECT t1.date, t1.home_confinement_cases AS national_cases, t2.home_confinement_cases AS piemonte_cases
FROM `bigquery-public-data.covid19_italy.national_trends`t1
RIGHT JOIN `bigquery-public-data.covid19_italy.data_by_region`t2 on t1.date = t2.date
AND t1.country = t2.country where t1.country = 'ITA' AND t2.region_name = 'Piemonte';
```
![image](https://github.com/lyudmilabaruah/lyudmilabaruah/assets/154314534/27cd71ea-e2b4-4140-86c2-78937c80efc2)













