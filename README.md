# Project Report

**1. Data Quality & Preprocessing**  

**Duplicate Handling**  
The dataset was checked for duplicate rows:  
Duplicate records were found and removed.  
After cleaning, duplicate count dropped to 0, ensuring data integrity.   


**Null Value Assessment**  
Null values were identified using .isnull() and visualized with a heatmap.  
Several columns such as Director, Cast, and Country contained missing values.  
For analyses requiring these fields, a cleaned dataset (data_new) was created by removing rows with null values.   


**2. Exploratory Data Analysis**  

**Dataset Composition: Movies vs TV Shows**
Using a group-by count and count-plot:  
Movies significantly outnumber TV Shows.  
This reflects Netflix’s acquisition and production strategy which historically had a larger focus on movies.   

**- Most Productive Directors**

The top 10 directors (by number of titles on Netflix) were extracted using value_counts().head(10):  
These directors have the highest total contributions of Movies/TV Shows on Netflix.  
Names vary from high-output documentary producers to filmmakers whose catalogues Netflix has licensed.   


**- Release Trends Over Time**

The results show:  
A strong surge in new titles during 2017–2020.  
This aligns with Netflix’s global expansion and increase in original content production.  
The dataset indicates that the year with the highest number of releases is near the late 2010s.  

A bar chart visualized year-wise counts, highlighting Netflix’s rapid content growth. 
![](https://github.com/XeNoX36/Netflix-Analysis-Project/blob/main/yearly%20netflix.png)


**- Country-Specific Insights**  
TV Shows Released in India Only  
Filtering TV Shows by country:  

India contributes a significant number of locally produced TV shows.  

These include Hindi-language series and regional language titles.  


**- Country with the Highest Number of TV Shows**  

Using value_counts:  

The United States has the highest number of TV Shows.  
After exploding, the U.S. remains the dominant contributor, followed by other major markets such as the U.K., Japan, and India.  


**- Movies Released in 2020**

Filtering:
```python
data[(data['Category']=='Movie') & (Year==2020)]
```
Shows all movies released in 2020.  

The year saw a large spike in content due to pandemic-related shifts in streaming demand.   


**- Category: Movie + Type:** Comedies OR Country = United Kingdom
A combined filter was used:  
Many comedy movies match the condition.  

Additionally, U.K.-produced content forms a large share due to strong licensing agreements between Netflix and British studios.  

**- How Many Movies/Shows Feature Tom Cruise?**

Two steps:  

Initial filter on exact match fails because cast lists contain multiple names.  

After dropping null values, .str.contains('Tom Cruise') identifies all titles in which he appears.  

The dataset includes a small number of Tom Cruise titles due to licensing restrictions (most are held by other platforms). 

**- Maximum Duration of a Title**  

Duration values were split:
```python
data[['Minutes','Unit']] = data['Duration'].str.split(' ', expand=True)
```
Converted minutes to integer, then extracted maximum.

Longest title duration belongs to either: 

Documentary extended cuts, or

Series labeled in terms of "Seasons" rather than minutes.  


**- TV Shows Rated 'R' After 2018**
Although the notebook uses Canada as a filter (likely unintended), the query shows:  
Very few "R"-rated TV Shows exist because R-rating applies mainly to movies.   
Most mature TV content uses TV-MA rating instead.   
Etlproject


**3. Key Insights Summary**
- Netflix’s library is dominated by Movies — both historically and in recent additions.  
- Release volume peaked in the late 2010s, reflecting Netflix’s aggressive expansion.  
- The U.S. leads content production, followed by India, U.K., Japan, and Canada.   
- Certain directors contribute disproportionately, likely due to documentary series or multi-episode shows.  
- The dataset includes multiple multi-country titles, requiring exploding for accurate country counts.  
- Tom Cruise appears in only a few Netflix titles, reflecting licensing limitations.   
- Content durations vary widely, with the longest being multi-episode series or long-form documen  taries.  
- Genre-country filters reveal strong clusters, such as U.K. comedies on Netflix.  
