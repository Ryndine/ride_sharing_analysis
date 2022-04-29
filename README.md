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

## Ride sharing analysis:
