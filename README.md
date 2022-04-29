# Ride Sharing Analysis

## Objective: 
The goal of this project is to gain insight and create simple visualizations for ride sharing data from 2019.

## Tools & databases used:
- Jupyter
- Pandas
- Matplotlib

## Preparing analysis:

**Cleaning with pandas:**

I looked over the dataset, checked for nulls, data types, and overall the data was clean. Minor adjustments needed for presentations but decided to put those off until they're ready for visualization.

For merging the two dataframe city was the only common column so I did a simple left merge.

**Organizing the data:**

Average fare vs total number of rides per city.
- Created a dataframe for each city type, then created three groups for each city type.
 1) Number of rides per city for each city type.
2) Average fare per city for each city type.
3) Average number of drivers for each city type.
- I then took these groupings and created a bubble chart which best visualizes all three of these variables.
- After visualization I created a statistical summary for each city type which gives me good initial insight into what the data may contain.

Detailed analysis:
- For a more in depth analysis I needed to find the central tendency for three groups of data:
1) Ride count for each city type.
2) Average fare for each city type.
3) Number of drivers for each city type
- From here I'm able to create box and whisker plots to show more detailed numbers and the range of the data.

Percentage of rides by type of city:
- I want to create more clear visuals in regards to how many rides each city type contains.
- For this data I'm grouping by city types and counting the ride_id, then dividing that by the total ride_id.
- Once converted to percentage I put together a pie chart for each city type to clearly show average rides per city.

Total weekly fares for each city type:
- For this analysis I needed to do a groupby, sum and pivot on the data. Then convert the data into a datatime so I could group on the weeks in order to find the sum of fares per week.
```
sum_fare_by_type = merged_data_df.groupby(["type", "date"]).sum()[["fare"]] \
                                .reset_index() \
                                .pivot(index="date", columns="type", values="fare")

fares_Jan_April = sum_fare_by_type.loc['2019-01-01':'2019-04-28']
fares_Jan_April.index = pd.to_datetime(fares_Jan_April.index)
weekly_fares_df = fares_Jan_April.resample('W').sum()
```
- From here I'm able to create a line plot to properly easily visualize the data over time.

## Ride data:

<img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/ride_share_data.png" width="75%" height="75%">  
With this analysis I'm looking at the general overview of data provided. There is a linear trend where areas with less population have fewer rides at a higher cost than more populated areas. Going forward I want to break down this data into smaller pieces for better visualizing this trend.

<img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/ride_count_data.png" width="75%" height="75%">  
As we see with this box and whisker plot Urban areas do have significantly more ride data than other city types. This dataset may not be the best representation of a rural area due to the low amount of data provided, but for what I have there is a strong correlation between the population density and the amount of rides cities have.

<img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/ride_fare_data.png" width="75%" height="75%">  
Here we see that rural areas do in fact have higher costs on average compared to the other city types. There may be correlation between travel distances since rural areas are more spread out. Further analysis on that would be required.

<img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/driver_count_data.png" width="75%" height="75%">  
Lastly I wanted to look into the individual driver count for each city type. As expected because Urban cities have much more activity, they also have many more drivers for their area as well. Same for Rural areas,there is a strong correlation between the amount of rides being given and the amount of drivers available.
<br/><br/>
<table>
  <!-- Optional table row if you want to have headers for each image -->
  <tr>
    <td>% of Total Fares by City Type</td>
    <td>% of Total Rides by City Type</td>
    <td>% of Total Drivers by City Type</td>
  </tr>
  <!-- This table row for the images you want aligned -->
  <tr>
    <td><img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/perc_type_pie.png" width="100%" height="100%"></td>
    <td><img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/perc_ride_pie.png" width="100%" height="100%"></td>
    <td><img src="https://github.com/Ryndine/ride_sharing_analysis/blob/main/Analysis/perc_drivers_pie.png" width="100%" height="100%"></td>
  </tr>
 </table>
