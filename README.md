# Oahu_Weather_Analysis
Using SQLite and SQLAlchemy to perform weather and statstical analysis in Oahu.

## Overview 
An investor would like to see the probability of a sustainable surf-shop in the island of Oahu. Weather analysis will be performed to determine if Ohau is an optimal location for the business. The data is stored in an SQLite file and queries must be performed using SQLAlchemy in Python. The analysis will focus on temperature data, described using summary statistics, for the months of June and December in Oahu. The data points span 7 years, from 2010 to 2017. 

The code file including the process to dervice the results can be found as [SurfsUp_Challenge](https://github.com/Fabalin/surfs_up/blob/main/SurfsUp_Challenge.ipynb). 

## Software
- Anaconda - 4.11.0
- Jupyter Notebook - 6.4.8
- Python - 3.7.11
### Key Dependencies in Python
- Pandas - 1.4.1
- SQLAlchemy - 1.4.35

## Results
The analysis was performed using a session engine that queries the SQLite data file using queries. Since the analysis is the same for both months, the code for performing the queries is quite similar. The deviation comes from the filter statement that uses the extract function from SQLAlchemy to look for temperatures associated with the months in question. 
```
# 2. Write a query that filters the Measurement table to retrieve the temperatures for the month of June. 
june_temp = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date) == '06').all()
```
The code above saves the results to a variable and the query is retured as a list. This is confirmed by using the `type()` function on the results variable. 

![list_confirm](https://github.com/Fabalin/surfs_up/blob/main/Resources/list_confirm.PNG)

Prior to obtaining the summary statistics, the results variable is converted to a dataframe for ease of analysis:
```
# 4. Create a DataFrame from the list of temperatures for the month of June. 
june_temp_df = pd.DataFrame(june_temp, columns=['date','June_Temps_(F)'])
june_temp_df.set_index(june_temp_df['date'], inplace=True)
```
The results are then reported as summary statistic tables: 

- June temperatures across the 7 years have an average of 74 degrees Farenheit with a minimum of 64 and a maximum of 85. The temperatures indicate a quintessential summer weather that is perfect for a surf shop. 
  
  ![June_Temps](https://github.com/Fabalin/surfs_up/blob/main/Resources/June_Temps.PNG)

- December temperatures are also on par with June temperatures with an average of 71 degrees Farenheight and a maximum of 83. The minimum temperature of 56 F appears to be an outlier as the quartiles are all higher temperatures. Since December can be taken as a proxy for the height of winter, the frequency of warm temperatures indicate that the surf shop is viable all year round. 

  ![December_Temps](https://github.com/Fabalin/surfs_up/blob/main/Resources/December_Temps.PNG)

## Summary 
The exploratory analysis performed in the [climate_analysis](https://github.com/Fabalin/surfs_up/blob/main/climate_analysis.ipynb) file along with the temperature analysis reported here both indicate that Oahu is an optimal location for opening up a surf shop. Temperatures are frequently warm and the precipitation per day frequently rests within 3 inches, with a few outliers in the last year, indicating a good tropical beach climate.  

Additional queries can be performed to further bolster this claim by coupling precipitation data to the temperature for June and December. Furthermore, this could be expanded to produce precipitation data for each month over the span of the available dataset to provide more insight into heavy rainfall months. This could help predict possible months with low foot traffic and low revenue to help allocate resources accordingly. 
