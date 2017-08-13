

```python
#homework 4 PyBer - import library 

import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

```


```python
#read csv file
city = "raw_data/city_data.csv"
ride = "raw_data/ride_data.csv"

```


```python
# Read our Data file with the pandas library
# Not every CSV requires an encoding, but be aware this can come up
ride_df = pd.read_csv(ride, encoding = "ISO-8859-1")
ride_df= ride_df.drop_duplicates()
ride_df.head()

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# read the second csv file

city_df = pd.read_csv(city, encoding = "ISO-8859-1")
city_df = city_df.drop_duplicates()
city_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>



#Read the seond csv file
city_df = pd.read_csv(city, encoding = "ISO-8859-1")
city_df.head()




```python
#join two data tables into one by city
sum_df = pd.merge(city_df, ride_df, on='city')
sum_df = sum_df.drop_duplicates()
sum_df.head()

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>7466473222333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>2140501382736</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>1896987891309</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>8784212854829</td>
    </tr>
  </tbody>
</table>
</div>




```python
# * Average Fare ($) Per City 
avg_ride = sum_df.groupby('city')['fare'].mean()
avg_ride.head()
```




    city
    Alvarezhaven    23.928710
    Alyssaberg      20.609615
    Anitamouth      37.315556
    Antoniomouth    23.625000
    Aprilchester    21.981579
    Name: fare, dtype: float64




```python
avg_ride_df= pd.DataFrame(avg_ride)
avg_ride_df.rename(columns={'city': 'city', 'fare': 'Avg_Fare'}, inplace=True)
avg_ride_df.reset_index(level=0, inplace=True)
avg_ride_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Avg_Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
    </tr>
  </tbody>
</table>
</div>




```python
#* Total Number of Rides Per City
Total_rides = sum_df.groupby('city').ride_id.count()

Total_rides.head()

```




    city
    Alvarezhaven    31
    Alyssaberg      26
    Anitamouth       9
    Antoniomouth    22
    Aprilchester    19
    Name: ride_id, dtype: int64




```python
Total_rides_df= pd.DataFrame(Total_rides)
Total_rides_df.rename(columns={'city': 'city', 'ride_id': 'Total_ride'}, inplace=True)
Total_rides_df.reset_index(level=0, inplace=True)
Total_rides_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Total_ride</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
#* Total Number of Drivers Per City
num_driver = city_df.groupby('city').driver_count.sum()
num_driver.head()

```




    city
    Alvarezhaven    21
    Alyssaberg      67
    Anitamouth      16
    Antoniomouth    21
    Aprilchester    49
    Name: driver_count, dtype: int64




```python
num_driver_df= pd.DataFrame(num_driver)
num_driver_df.rename(columns={'city': 'city', 'driver_count': 'Total_driver'}, inplace=True)
num_driver_df.reset_index(level=0, inplace=True)
num_driver_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Total_driver</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>21</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>16</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>49</td>
    </tr>
  </tbody>
</table>
</div>




```python
#* City Type (Urban, Suburban, Rural)
city_type = city_df[["city","type"]]
city_type.head()

                    
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# fin_df = avg_ride_df.join(Total_rides_df, on = ['city'], how = 'inner')

fin_df = pd.merge(avg_ride_df, Total_rides_df, on='city')
fin_df = pd.merge(fin_df, num_driver_df, on='city')
fin_df = pd.merge(fin_df, city_type, on='city')
fin_df.head()

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Avg_Fare</th>
      <th>Total_ride</th>
      <th>Total_driver</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
      <td>31</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
      <td>26</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
      <td>9</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
      <td>22</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
      <td>19</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#plot the following variables:

# x axis = number of ride per city
# y axis = average fair per city
# color = city type per city
# s = diver count per city

colors = ["LightCoral", "LightSkyBlue", "Gold"]
sns.set_palette(colors,3,0.75)


#plot data for urban city type
urban = fin_df.loc[fin_df['type'] == "Urban"]
urbanplt = plt.scatter(urban["Total_ride"], urban["Avg_Fare"], marker="o", s=urban["Total_driver"], label='Urban',edgecolor = "b", linewidths=0.75,alpha=0.75)

# plot data for Suburban city type
Suburban = fin_df.loc[fin_df['type'] == "Suburban"]
suburbanplt= plt.scatter(Suburban["Total_ride"], Suburban["Avg_Fare"], marker="o", s=Suburban["Total_driver"],label='Suburban', edgecolor = "b",alpha=0.75)

# plot data for Rural city type
Rural = fin_df.loc[fin_df['type'] == "Rural"]
ruralplt = plt.scatter(Rural["Total_ride"], Rural["Avg_Fare"], marker="o", s=Rural["Total_driver"],label='Rural', edgecolor = "b",alpha=0.75)

#titles,lables, and legends
plt.title("PyBer RideSharing Data (2016)")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")

plt.legend(handles = [urbanplt, suburbanplt, ruralplt],title="City types", loc = "upper right")

# Show plot
plt.show()

```


![png](output_14_0.png)



```python
# In addition, you will be expected to produce the following three pie charts:
# * % of Total Fares by City Type

#Create a new column to define the fare per city
fin_df["fare_per_city"]=""
for index, row in fin_df.iterrows():
     fin_df.set_value(index, "fare_per_city", row["Avg_Fare"]* row["Total_ride"])
        
#define the total fare for each city type

urban_fare = fin_df.loc[fin_df['type'] == "Urban"]
urban_fare_total = round(urban_fare["fare_per_city"].sum(),2)

Suburban_fare = fin_df.loc[fin_df['type'] == "Suburban"]
Suburban_fare_total = round(Suburban_fare["fare_per_city"].sum(),2)

Rural_fare = fin_df.loc[fin_df['type'] == "Rural"]
Rural_fare_total = round(Rural_fare["fare_per_city"].sum(),2)

#create a new dataframe to store the total fare per type
new_data = {"type":["Urban","Suburban", "Rural"], "total_fare":[urban_fare_total,Suburban_fare_total,Rural_fare_total]}
fare=pd.DataFrame(new_data)

# plot pie chart
plt.pie(fare["total_fare"], labels=fare["type"], shadow=True,explode=(0.15, 0, 0),startangle=200, autopct='%1.1f%%')
plt.title("% of Total Fares by City Type")
plt.tight_layout()
plt.show()

```


![png](output_15_0.png)



```python
# * % of Total Rides by City Type
        
#define the total ride for each city type

urban_total_ride = round(urban_fare["Total_ride"].sum(),2)
Suburban_total_ride = round(Suburban_fare["Total_ride"].sum(),2)
Rural_total_ride = round(Rural_fare["Total_ride"].sum(),2)

#create a new dataframe to store the total fare per city type
new_data = {"type":["Urban","Suburban", "Rural"], "total_rides":[urban_total_ride,Suburban_total_ride,Rural_total_ride]}
ride=pd.DataFrame(new_data)

# plot pie chart
plt.pie(ride["total_rides"], labels=fare["type"], shadow=True,explode=(0.15, 0, 0),startangle=200, autopct='%1.1f%%')
plt.title("% of Total Rides by City Type")
plt.tight_layout()
plt.show()

```


![png](output_16_0.png)



```python
# * % of Total Drivers by City Type

#define the total driver for each city type

urban_driver = urban_fare["Total_driver"].sum()
Suburban_driver = Suburban_fare["Total_driver"].sum()
Rural_driver = Rural_fare["Total_driver"].sum()

#create a new dataframe to store the total fare per city type
new_data = {"type":["Urban","Suburban", "Rural"], "total_drivers":[urban_driver,Suburban_driver,Rural_driver]}
driver=pd.DataFrame(new_data)

# plot pie chart
plt.pie(driver["total_drivers"], labels=fare["type"], shadow=True,explode=(0.15, 0, 0),startangle=200, autopct='%1.1f%%')
plt.title("% of Total Drivers by City Type")
plt.tight_layout()
plt.show()


```


![png](output_17_0.png)



```python

```
