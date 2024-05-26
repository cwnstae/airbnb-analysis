# Airbnb Analysis
Welcome to this Airbnb analysis, designed to showcase the comprehensive skills required for data analytics. In this project, I will utilize various tools to manipulate the "Insight Airbnb Dataset 8 Apr 2024" ([link](https://insideairbnb.com/get-the-data/)). Airbnb listings are created by hosts who want to rent out their properties to travelers and other short-term guests. The listings can vary widely in terms of type, price, location, and amenities offered.

## What you will see
In this showcase, I will cover various methods to tackle this large dataset, including data cleaning, data formatting, and creating a database for SQL demonstrations. You will see how I manipulate the data using Python, and finally, I will summarize and describe the insights derived from the data. I will also create a visualization dashboard using Tableau.

## Key skills showcased
 - Python (pandas): The primary tool I use to manipulate and format the data.
 - SQL: Used to create a database and demonstrate querying for data exploration.
 - Tableau: Utilized to interpret and present the insightful data in an understandable manner through graphs and dashboards.

# Loading and exporing data
In this section, we will load the data and explore it to understand the details before conducting any analysis. We will identify and handle dirty data, and format it into usable data. The dataset we are using is `listings.csv`, `calendar.csv`, and `reviews,csv`.

```python
current_path = str(Path().absolute())
df_listings = pd.read_csv(current_path + "\data - listings.csv")
df_listings.info()
df_listings
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 395 entries, 0 to 394
Data columns (total 75 columns):
 #   Column                                        Non-Null Count  Dtype  
---  ------                                        --------------  -----  
 0   id                                            395 non-null    int64  
 1   listing_url                                   395 non-null    object 
 2   scrape_id                                     395 non-null    int64  
 3   last_scraped                                  395 non-null    object 
 4   source                                        395 non-null    object 
 5   name                                          395 non-null    object 
 6   description                                   385 non-null    object 
 7   neighborhood_overview                         235 non-null    object 
 8   picture_url                                   395 non-null    object 
 9   host_id                                       395 non-null    int64  
 10  host_url                                      395 non-null    object 
 11  host_name                                     395 non-null    object 
 12  host_since                                    395 non-null    object 
 13  host_location                                 301 non-null    object 
 14  host_about                                    206 non-null    object 
 15  host_response_time                            370 non-null    object 
 16  host_response_rate                            370 non-null    object 
 17  host_acceptance_rate                          381 non-null    object 
 18  host_is_superhost                             390 non-null    object 
 19  host_thumbnail_url                            395 non-null    object 
...
 73  calculated_host_listings_count_shared_rooms   395 non-null    int64  
 74  reviews_per_month                             352 non-null    float64
dtypes: float64(18), int64(23), object(34)
memory usage: 231.6+ KB
```
<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>listing_url</th>
      <th>scrape_id</th>
      <th>last_scraped</th>
      <th>source</th>
      <th>name</th>
      <th>description</th>
      <th>neighborhood_overview</th>
      <th>picture_url</th>
      <th>host_id</th>
      <th>...</th>
      <th>review_scores_communication</th>
      <th>review_scores_location</th>
      <th>review_scores_value</th>
      <th>license</th>
      <th>instant_bookable</th>
      <th>calculated_host_listings_count</th>
      <th>calculated_host_listings_count_entire_homes</th>
      <th>calculated_host_listings_count_private_rooms</th>
      <th>calculated_host_listings_count_shared_rooms</th>
      <th>reviews_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1489424</td>
      <td>https://www.airbnb.com/rooms/1489424</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Welcoming, easygoing, comfy bed, entire level</td>
      <td>Queen size bed, extra comfy mattress, with acc...</td>
      <td>Quiet yet convenient.</td>
      <td>https://a0.muscache.com/pictures/21977748/1dc8...</td>
      <td>5294164</td>
      <td>...</td>
      <td>4.92</td>
      <td>4.82</td>
      <td>4.81</td>
      <td>NaN</td>
      <td>f</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1.93</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2992450</td>
      <td>https://www.airbnb.com/rooms/2992450</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Luxury 2 bedroom apartment</td>
      <td>The apartment is located in a quiet neighborho...</td>
      <td>NaN</td>
      <td>https://a0.muscache.com/pictures/44627226/0e72...</td>
      <td>4621559</td>
      <td>...</td>
      <td>4.56</td>
      <td>3.22</td>
      <td>3.67</td>
      <td>NaN</td>
      <td>f</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3820211</td>
      <td>https://www.airbnb.com/rooms/3820211</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Restored Precinct in Center Sq. w/Parking</td>
      <td>Cozy, cool little 1BR Apt in the heart Albany'...</td>
      <td>Great restaurants, architecture, walking, peop...</td>
      <td>https://a0.muscache.com/pictures/prohost-api/H...</td>
      <td>19648678</td>
      <td>...</td>
      <td>4.81</td>
      <td>4.82</td>
      <td>4.79</td>
      <td>NaN</td>
      <td>f</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2.53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5651579</td>
      <td>https://www.airbnb.com/rooms/5651579</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Large studio apt  by Capital Center &amp; ESP@</td>
      <td>Spacious studio with hardwood floors, fully eq...</td>
      <td>The neighborhood is very eclectic. We have a v...</td>
      <td>https://a0.muscache.com/pictures/b3fc42f3-6e5e...</td>
      <td>29288920</td>
      <td>...</td>
      <td>4.87</td>
      <td>4.79</td>
      <td>4.64</td>
      <td>NaN</td>
      <td>f</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>3.13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6623339</td>
      <td>https://www.airbnb.com/rooms/6623339</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Center Sq. Loft in Converted Precinct w/ Parking</td>
      <td>Large renovated 1 bedroom apartment in convert...</td>
      <td>Located in Albany's finest urban neighborhood,...</td>
      <td>https://a0.muscache.com/pictures/prohost-api/H...</td>
      <td>19648678</td>
      <td>...</td>
      <td>4.69</td>
      <td>4.81</td>
      <td>4.72</td>
      <td>NaN</td>
      <td>f</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2.88</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>390</th>
      <td>1124558577325015506</td>
      <td>https://www.airbnb.com/rooms/1124558577325015506</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Charming 1BR Near Capitol-Dwntwn</td>
      <td>This is a cozy, well appointed garden level ap...</td>
      <td>NaN</td>
      <td>https://a0.muscache.com/pictures/miso/Hosting-...</td>
      <td>46312980</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>391</th>
      <td>1124632058968031818</td>
      <td>https://www.airbnb.com/rooms/1124632058968031818</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Modern Duplex - Historical Home</td>
      <td>Modern townhouse across from the Governors man...</td>
      <td>NaN</td>
      <td>https://a0.muscache.com/pictures/miso/Hosting-...</td>
      <td>46312980</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>392</th>
      <td>1128332989288304495</td>
      <td>https://www.airbnb.com/rooms/1128332989288304495</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Downtown Albany Vacation Rental - Chic &amp; Walka...</td>
      <td>Experience the best of Albany from 'Duckies Ca...</td>
      <td>DOWNTOWN DESTINATIONS: Albany Capital Center (...</td>
      <td>https://a0.muscache.com/pictures/prohost-api/H...</td>
      <td>121680792</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>t</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>393</th>
      <td>1128386510439836615</td>
      <td>https://www.airbnb.com/rooms/1128386510439836615</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Welcome home travelers</td>
      <td>Peaceful, relaxing yet convenient.  Our 1 bedr...</td>
      <td>NaN</td>
      <td>https://a0.muscache.com/pictures/miso/Hosting-...</td>
      <td>502037254</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>394</th>
      <td>1129005873707096339</td>
      <td>https://www.airbnb.com/rooms/1129005873707096339</td>
      <td>20240408160234</td>
      <td>2024-04-08</td>
      <td>city scrape</td>
      <td>Walk to Albany Med &amp; Restaurants</td>
      <td>Two bedroom apartment walkable to Albany Medic...</td>
      <td>NaN</td>
      <td>https://a0.muscache.com/pictures/af754e5c-5b0b...</td>
      <td>30883612</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>395 rows × 75 columns</p>
</div>

There are a total of 75 columns, but we don't need all of them.

```python
# The listings has 75 columns, select some columns
selected_listings = df_listings.copy()
selected_listings = selected_listings[["id","latitude","longitude","room_type","bathrooms","bedrooms","number_of_reviews","price"]]
 # clean data from $5,500.00 to 5500.0
selected_listings["price"] = selected_listings["price"].str.replace("$","")
selected_listings["price"] = selected_listings["price"].str.replace(",","")
selected_listings["price"] = selected_listings["price"].astype(float)
selected_listings.to_csv(current_path + "\data - selected_listings.csv",index=False) # Export to csv for creating SQL database
selected_listings
```
<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>room_type</th>
      <th>bathrooms</th>
      <th>bedrooms</th>
      <th>number_of_reviews</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1489424</td>
      <td>42.667190</td>
      <td>-73.815800</td>
      <td>Private room</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>248</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2992450</td>
      <td>42.657890</td>
      <td>-73.753700</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>9</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3820211</td>
      <td>42.652220</td>
      <td>-73.767240</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>297</td>
      <td>115.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5651579</td>
      <td>42.646150</td>
      <td>-73.759660</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>340</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6623339</td>
      <td>42.652220</td>
      <td>-73.767240</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>310</td>
      <td>115.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>390</th>
      <td>1124558577325015506</td>
      <td>42.646032</td>
      <td>-73.760482</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>391</th>
      <td>1124632058968031818</td>
      <td>42.646032</td>
      <td>-73.760482</td>
      <td>Entire home/apt</td>
      <td>1.5</td>
      <td>1.0</td>
      <td>0</td>
      <td>110.0</td>
    </tr>
    <tr>
      <th>392</th>
      <td>1128332989288304495</td>
      <td>42.657838</td>
      <td>-73.753822</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>106.0</td>
    </tr>
    <tr>
      <th>393</th>
      <td>1128386510439836615</td>
      <td>42.648930</td>
      <td>-73.768859</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>394</th>
      <td>1129005873707096339</td>
      <td>42.654450</td>
      <td>-73.789242</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
<p>395 rows × 8 columns</p>
</div>

```python
df_calendar = pd.read_csv(current_path + "\data - calendar.csv")
df_calendar["available"] = df_calendar["available"].astype(bool) # convert to boolean datatype
df_calendar.to_csv(current_path + "\data - calendar_1.csv", index=False)
df_calendar.info()
df_calendar
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 144175 entries, 0 to 144174
Data columns (total 7 columns):
 #   Column          Non-Null Count   Dtype  
---  ------          --------------   -----  
 0   listing_id      144175 non-null  int64  
 1   date            144175 non-null  object 
 2   available       144175 non-null  bool   
 3   price           144175 non-null  object 
 4   adjusted_price  0 non-null       float64
 5   minimum_nights  144175 non-null  int64  
 6   maximum_nights  144175 non-null  int64  
dtypes: bool(1), float64(1), int64(3), object(2)
memory usage: 6.7+ MB
```
<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>listing_id</th>
      <th>date</th>
      <th>available</th>
      <th>price</th>
      <th>adjusted_price</th>
      <th>minimum_nights</th>
      <th>maximum_nights</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1489424</td>
      <td>2024-04-08</td>
      <td>True</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>1125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1489424</td>
      <td>2024-04-09</td>
      <td>True</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>1125</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1489424</td>
      <td>2024-04-10</td>
      <td>True</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>1125</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1489424</td>
      <td>2024-04-11</td>
      <td>True</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>1125</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1489424</td>
      <td>2024-04-12</td>
      <td>True</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>1125</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>144170</th>
      <td>1129005873707096339</td>
      <td>2025-04-03</td>
      <td>True</td>
      <td>60.0</td>
      <td>NaN</td>
      <td>30</td>
      <td>365</td>
    </tr>
    <tr>
      <th>144171</th>
      <td>1129005873707096339</td>
      <td>2025-04-04</td>
      <td>True</td>
      <td>60.0</td>
      <td>NaN</td>
      <td>30</td>
      <td>365</td>
    </tr>
    <tr>
      <th>144172</th>
      <td>1129005873707096339</td>
      <td>2025-04-05</td>
      <td>True</td>
      <td>60.0</td>
      <td>NaN</td>
      <td>30</td>
      <td>365</td>
    </tr>
    <tr>
      <th>144173</th>
      <td>1129005873707096339</td>
      <td>2025-04-06</td>
      <td>True</td>
      <td>60.0</td>
      <td>NaN</td>
      <td>30</td>
      <td>365</td>
    </tr>
    <tr>
      <th>144174</th>
      <td>1129005873707096339</td>
      <td>2025-04-07</td>
      <td>True</td>
      <td>60.0</td>
      <td>NaN</td>
      <td>30</td>
      <td>365</td>
    </tr>
  </tbody>
</table>
<p>144175 rows × 7 columns</p>
</div>

```python
df_reviews = pd.read_csv(current_path + "\data - reviews.csv")
df_reviews.info()
df_reviews
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 22410 entries, 0 to 22409
Data columns (total 6 columns):
 #   Column         Non-Null Count  Dtype 
---  ------         --------------  ----- 
 0   listing_id     22410 non-null  int64 
 1   id             22410 non-null  int64 
 2   date           22410 non-null  object
 3   reviewer_id    22410 non-null  int64 
 4   reviewer_name  22410 non-null  object
 5   comments       22404 non-null  object
dtypes: int64(3), object(3)
memory usage: 1.0+ MB
```


<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>listing_id</th>
      <th>id</th>
      <th>date</th>
      <th>reviewer_id</th>
      <th>reviewer_name</th>
      <th>comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1489424</td>
      <td>7208791</td>
      <td>2013-09-10</td>
      <td>5817914</td>
      <td>Hilary</td>
      <td>Efrat and Dan were very welcoming and accommod...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1489424</td>
      <td>8001939</td>
      <td>2013-10-12</td>
      <td>4786919</td>
      <td>Sharon</td>
      <td>As advertised, a very comfy bed. Restful room,...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1489424</td>
      <td>8123022</td>
      <td>2013-10-16</td>
      <td>4786919</td>
      <td>Sharon</td>
      <td>Glad to be back for a second time in my cozy r...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1489424</td>
      <td>8279957</td>
      <td>2013-10-23</td>
      <td>8362214</td>
      <td>Andrej</td>
      <td>We stayed only for a night, so can not tell mu...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1489424</td>
      <td>8303182</td>
      <td>2013-10-24</td>
      <td>9458270</td>
      <td>Andreia</td>
      <td>I had a pleasant stay here. The bed was indeed...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>22405</th>
      <td>1104977057298366617</td>
      <td>1129794827864199140</td>
      <td>2024-04-07</td>
      <td>201370147</td>
      <td>Rodney</td>
      <td>Thomas place was great, comfortable, bright an...</td>
    </tr>
    <tr>
      <th>22406</th>
      <td>1111221935683053416</td>
      <td>1118936295025008739</td>
      <td>2024-03-23</td>
      <td>72720260</td>
      <td>Jean-Francois</td>
      <td>Nouveau sur AirBnb, donc tout les accessoires ...</td>
    </tr>
    <tr>
      <th>22407</th>
      <td>1111221935683053416</td>
      <td>1120334433573933434</td>
      <td>2024-03-25</td>
      <td>389293711</td>
      <td>Mary</td>
      <td>I stayed here while going to a concert with my...</td>
    </tr>
    <tr>
      <th>22408</th>
      <td>1111221935683053416</td>
      <td>1126098924470824799</td>
      <td>2024-04-02</td>
      <td>77260245</td>
      <td>Audrey</td>
      <td>Stephanie was easy to reach and always helpful...</td>
    </tr>
    <tr>
      <th>22409</th>
      <td>1120212616553191970</td>
      <td>1124701306946103180</td>
      <td>2024-03-31</td>
      <td>458919181</td>
      <td>Jenny</td>
      <td>Beautiful place. Very clean and the host so at...</td>
    </tr>
  </tbody>
</table>
<p>22410 rows × 6 columns</p>
</div>

## Creating Database
Before going further, as I mentioned earlier, I intend to use SQL to manipulate the data. In this section, I have already prepared the necessary setup using PostgreSQL. However, we won't focus on that right now. The table I created is detailed below.
```sql
-- Create listings table
CREATE TABLE public.listings
(
    id BIGINT PRIMARY KEY,
    latitude NUMERIC,
    longitude NUMERIC,
    room_type TEXT,
    bathrooms NUMERIC,
    bedrooms NUMERIC,
    number_of_reviews INT,
    price NUMERIC
);

-- Create calendar table
CREATE TABLE public.calendar
(
    listing_id BIGINT,
    date DATE,
    available BOOLEAN,
    price NUMERIC,
    adjusted_price NUMERIC,
    minimum_nights INT,
    maximum_nights INT,
    FOREIGN KEY (listing_id) REFERENCES public.listings (id)
);

-- Create reviews table
CREATE TABLE public.reviews
(
    listing_id BIGINT,
    id BIGINT PRIMARY KEY,
    date DATE,
    reviewer_id INT,
    reviewer_name TEXT,
    comments TEXT,
    FOREIGN KEY (listing_id) REFERENCES public.listings (id)
);

```
## Exporing Data by SQL
I will use Python code to execute SQL queries. Let's set everything up.
```python
# Make connection with PostgresSQL server
con_string = f"postgresql://postgres:{encoded_password}@localhost:5432/Airbnb"
engine = create_engine(con_string)
```

```python
query = """
    SELECT *
    FROM listings;
"""
df_read_sql = pd.read_sql(query,engine)
df_read_sql
```
<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>room_type</th>
      <th>bathrooms</th>
      <th>bedrooms</th>
      <th>number_of_reviews</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1489424</td>
      <td>42.667190</td>
      <td>-73.815800</td>
      <td>Private room</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>248</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2992450</td>
      <td>42.657890</td>
      <td>-73.753700</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>9</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3820211</td>
      <td>42.652220</td>
      <td>-73.767240</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>297</td>
      <td>115.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5651579</td>
      <td>42.646150</td>
      <td>-73.759660</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>340</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6623339</td>
      <td>42.652220</td>
      <td>-73.767240</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>310</td>
      <td>115.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>390</th>
      <td>1124558577325015506</td>
      <td>42.646032</td>
      <td>-73.760482</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>391</th>
      <td>1124632058968031818</td>
      <td>42.646032</td>
      <td>-73.760482</td>
      <td>Entire home/apt</td>
      <td>1.5</td>
      <td>1.0</td>
      <td>0</td>
      <td>110.0</td>
    </tr>
    <tr>
      <th>392</th>
      <td>1128332989288304495</td>
      <td>42.657838</td>
      <td>-73.753822</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>106.0</td>
    </tr>
    <tr>
      <th>393</th>
      <td>1128386510439836615</td>
      <td>42.648930</td>
      <td>-73.768859</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>394</th>
      <td>1129005873707096339</td>
      <td>42.654450</td>
      <td>-73.789242</td>
      <td>Entire home/apt</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
<p>395 rows × 8 columns</p>
</div>

Everything looks perfect ready to get started.

## We'll be exploring what factors influence price differences.
### Room Type
```python
query = """
SELECT
    room_type,
    COUNT(*) as total_listed_room,
    ROUND(AVG(price),2) AS price_avg
FROM listings
WHERE price IS NOT NULL
GROUP BY room_type
;
"""
df_read_sql = pd.read_sql(query,engine)
df_read_sql
```
<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>room_type</th>
      <th>total_listed_room</th>
      <th>price_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Entire home/apt</td>
      <td>283</td>
      <td>142.10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Shared room</td>
      <td>2</td>
      <td>75.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Private room</td>
      <td>93</td>
      <td>84.06</td>
    </tr>
  </tbody>
</table>
</div>

There are 3 types of room:
 - Entire Home/Apartment: This category dominates with 283 listings and commands the highest average price of $142.10 per stay.
 - Private Room: Although less common, there are 93 private room listings, priced at an average of $84.06 half the cost of entire homes/apartments
 - Shared Room: The least prevalent, with only 2 listings, but offers the most economical stays at an average price of $75.00.

### Number of Bedroom

```python
query = """
SELECT
    bedrooms,
    COUNT(*) as total_listed_room,
    ROUND(AVG(price),2) AS price_avg,
    SUM(price) as total_revenue
FROM listings
WHERE bedrooms > 0 AND price IS NOT NULL
GROUP BY bedrooms
ORDER BY bedrooms
;
"""
df_read_sql = pd.read_sql(query,engine)
df_read_sql
```

<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bedrooms</th>
      <th>total_listed_room</th>
      <th>price_avg</th>
      <th>total_revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>211</td>
      <td>90.21</td>
      <td>19034.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>84</td>
      <td>129.68</td>
      <td>10893.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>41</td>
      <td>191.93</td>
      <td>7869.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>16</td>
      <td>222.94</td>
      <td>3567.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>9</td>
      <td>496.11</td>
      <td>4465.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.0</td>
      <td>1</td>
      <td>807.00</td>
      <td>807.0</td>
    </tr>
  </tbody>
</table>
</div>

There are number of bedrooms 1 - 7 rooms:
 - Single Bedroom (1 room): Despite having the lowest average price at $90.21, it generates the highest total revenue.
 - As the number of bedrooms increases, the average price rises, but the total revenue decreases.
 - In summary:
    - 1 bedroom: Lowest price, highest revenue.
    - Increasing bedrooms: Higher prices, lower revenue.

