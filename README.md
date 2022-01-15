# Surfs Up

## Overview of the statistical analysis:
  - Project was made to look at the temperature data for the months of June and December in Oahu, in order to determine if the surf and ice cream shop business is sustainable year-round in that area and possible reuse the code for other places around it. They way we did it was running two separed queries for June and December, stored it in a list and convert it to a DataFrame. Also, to get our summary statistics I used the .describe() method. 

## Results:
  - For the first query to show the weather in June: 

  ![This is an image](https://github.com/KandiJayana/surfs_up/blob/21319be9ff29733bfa00141ccf0b8aa46f34f397/June.png) 
  
  
  - For the second query to show the weather in December: 
  
  ![This is an image](https://github.com/KandiJayana/surfs_up/blob/21319be9ff29733bfa00141ccf0b8aa46f34f397/December.png)
  
### From the images above we can see the differences in weather between June and December:

  - The count for June is 10.76% more than December
  
  - The standard deviation for June is 13.04% more than December
  
  - The min temperature in June is 12.50% more than December

## Summary:
- From the results we can see that June was performed as a warmer monthly based on the data we collected that show an increase of  12.50% for the minimum temperature and an increase of 2.35% for the max temperature, but both of the seasons is still good for turism and outdoor activities like shopping. 

#### Additional queries that may provide more insight:
- Last 12 months of precipitation data:
prev_year = dt.date(2017, 8, 23) - dt.timedelta(days=365)
results = []
results = session.query(Measurement.date, Measurement.prcp).filter(Measurement.date >= prev_year)
df = pd.DataFrame(results, columns=['date','precipitation'])
df.set_index(df['date'], inplace=True)
df = df.sort_index()
df.plot()
- How many stations are available in this dataset:
session.query(func.count(Station.station)).all()
- What are the most active stations:
session.query(Measurement.station, func.count(Measurement.station)).\
group_by(Measurement.station).order_by(func.count(Measurement.station).desc()).all()
- The lowest temperature recorded:
session.query(func.min(Measurement.tobs), func.max(Measurement.tobs), func.avg(Measurement.tobs)).\
filter(Measurement.station == 'USC00519281').all()
