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
<img src="https://raw.githubusercontent.com/cwnstae/cwnstae.github.io/main/assets/Pic-Listings-1-2.png">

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
<img src="https://raw.githubusercontent.com/cwnstae/cwnstae.github.io/main/assets/Pic-Listings-2-1.png">

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
<img src="https://raw.githubusercontent.com/cwnstae/cwnstae.github.io/main/assets/Pic-Calendar-1-1.png">

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


<img src="https://raw.githubusercontent.com/cwnstae/cwnstae.github.io/main/assets/Pic-Reviews-1-1.png">

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
<img src="https://raw.githubusercontent.com/cwnstae/cwnstae.github.io/main/assets/Pic-SQL-1-1.png">
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
<table>
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


