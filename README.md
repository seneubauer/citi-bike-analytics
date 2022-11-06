# citi-bike-analytics

## Extract-Transform Process
I had to perform a variety of functions to prepare the raw [CitiBike data](https://ride.citibikenyc.com/system-data) into something Tableau can use easily. These steps are listed below.
1. Decide on what data to use. I ended up not using the most recent data as it didn't include what I wanted.
1. Reduce the raw data size to allow for a workable dataset. I decided on using ~500,000 records.
1. Apply universal datetime formatting to the relevant columns.
1. Calculate additional columns that would otherwise be clunky with Tableau's Calculated Fields.
1. Standardize column names across the 90+ data files.

These steps were accomplished in the accompanying Jupyter Notebook with Python. It is relatively simple; it iterates through the raw data CSVs where it opens, cleans, then stores a sampling into a new DataFrame. These new DataFrames were then stored in a list. After the iterator completes, the list is concated into a final DataFrame which is then saved to file.

The script executes reliably but had to account for messy raw data. For example, in some fields there were lone newline characters (\n) which caused issues with row cleaning. I also encountered at least one definite typo in the `birth_year` column: the value was 1885 so I assume the intended value was 1985. To combat this I introduced a filter to remove all rows where `birth_year` was less than 1920.

## Analysis
Once the data was cleaned and prepared for use, I loaded it into a [Tableau Workbook](https://public.tableau.com/views/citi-bike-analytics_16677144668210/YearlyUsage?:language=en-US&:display_count=n&:origin=viz_share_link) for visualization. 

### Yearly Usage
When one looks at the yearly usage trend, it is clear the program experienced a rapid increase in popularity fron 2014 to 2019. It is reasonable to assume the decrease in popularity from 2019 to 2020 is mostly due to the COVID-19 pandemic. The drastic drop in 2021 is due to the dataset provided (2021 dataset was incomplete due to formatting change).

### Monthly Usage
This trend shows how season influences CitiBike usage. NYC experiences cold winters, so it is reasonable to assume people prefer to stay indoors during the colder months. But during the pleasant fall months usage climbs steadily.

### Daily Usage
This trend shows how many people start a session during each hour of a day. The two spikes correspond with weekday morning/evening commutes. It was interesting to see how midnight experiences more usage than 4am; perhaps this is due to the large city's 'night life'.

### User Distribution
I wanted to see how age ranges influenced one's usage of the CitiBike program. From the `User Ages` plot one can see the most populous ages are younger adults (mid 20s to mid 30s). There is one spike at the 50s. This spike also shows it contains the users who have the longest rides. Perhaps there are more biking enthusiasts in this age range whereas the younger demographic uses it out of necessity.

### Station Popularity
This data is pretty straightforward. The aptly named `Popular Start Stations` and `Popular End Stations` plots show the most and least popular stations. If a station were to require special attention these would be the ones.

### Maps
The start and end station maps show the previous plots but in graphical form. Larger spots correspond with more popular stations.
