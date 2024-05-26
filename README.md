# Introduction
Welcome to this Airbnb analysis, designed to showcase the comprehensive skills required for data analytics. In this project, I will utilize various tools to manipulate the "Airbnb Listings 2016 Dataset" provided by Alex The Analyst ([link](https://www.kaggle.com/datasets/alexanderfreberg/airbnb-listings-2016-dataset)).

## What you will see
In this showcase, I will cover various methods to tackle this large dataset, including data cleaning, data formatting, and creating a database for SQL demonstrations. You will see how I manipulate the data using Python, and finally, I will summarize and describe the insights derived from the data. I will also create a visualization dashboard using Tableau.

## Key skills showcased
 - Python (pandas): The primary tool I use to manipulate and format the data.
 - SQL: Used to create a database and demonstrate querying for data exploration.
 - Tableau: Utilized to interpret and present the insightful data in an understandable manner through graphs and dashboards.

# Loading and exporing data
In this section, we will load the data and explore it to understand the details before conducting any analysis. We will identify and handle dirty data, and format it into usable data. The dataset we are using is `Tableau Full Project.xlsx`, which contains three sheets: `Listings`, `Calendar`, and `Reviews`.

```python
current_path = str(Path().absolute())
# Loading data from Listings sheet
df_listings = pd.read_excel(current_path + "\Tableau Full Project.xlsx",sheet_name="Listings")
df_listings.head()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 3818 entries, 0 to 3817
Data columns (total 92 columns):
 #   Column                            Non-Null Count  Dtype         
---  ------                            --------------  -----         
 0   id                                3818 non-null   int64         
 1   listing_url                       3818 non-null   object        
 2   scrape_id                         3818 non-null   int64         
 3   last_scraped                      3818 non-null   datetime64[ns]
 4   name                              3818 non-null   object        
 5   summary                           3639 non-null   object        
 6   space                             3249 non-null   object        
 7   description                       3818 non-null   object        
 8   experiences_offered               3818 non-null   object        
 9   neighborhood_overview             2786 non-null   object        
 10  notes                             2206 non-null   object        
 11  transit                           2883 non-null   object        
 12  thumbnail_url                     3498 non-null   object        
 13  medium_url                        3498 non-null   object        
 14  picture_url                       3818 non-null   object        
 15  xl_picture_url                    3498 non-null   object        
 16  host_id                           3818 non-null   int64         
 17  host_url                          3818 non-null   object        
 18  host_name                         3816 non-null   object        
 19  host_since                        3816 non-null   datetime64[ns]
 20  host_location                     3810 non-null   object        
 21  host_about                        2959 non-null   object        
 22  host_response_time                3295 non-null   object        
 23  host_response_rate                3295 non-null   float64       
 24  host_acceptance_rate              3045 non-null   float64       
 25  host_is_superhost                 3816 non-null   object        
 26  host_thumbnail_url                3816 non-null   object        
 27  host_picture_url                  3816 non-null   object        
 28  host_neighbourhood                3518 non-null   object        
 29  host_listings_count               3816 non-null   float64       
 30  host_total_listings_count         3816 non-null   float64       
 31  host_verifications                3816 non-null   object        
 32  host_has_profile_pic              3816 non-null   object        
 33  host_identity_verified            3816 non-null   object        
 34  street                            3818 non-null   object        
 35  neighbourhood                     3402 non-null   object        
 36  neighbourhood_cleansed            3818 non-null   object        
 37  neighbourhood_group_cleansed      3818 non-null   object        
 38  city                              3818 non-null   object        
 39  state                             3818 non-null   object        
 40  zipcode                           3811 non-null   object        
 41  market                            3818 non-null   object        
 42  smart_location                    3818 non-null   object        
 43  country_code                      3818 non-null   object        
 44  country                           3818 non-null   object        
 45  latitude                          3818 non-null   float64       
 46  longitude                         3818 non-null   float64       
 47  is_location_exact                 3818 non-null   object        
 48  property_type                     3817 non-null   object        
 49  room_type                         3818 non-null   object        
 50  accommodates                      3818 non-null   int64         
 51  bathrooms                         3802 non-null   float64       
 52  bedrooms                          3812 non-null   float64       
 53  beds                              3817 non-null   float64       
 54  bed_type                          3818 non-null   object        
 55  amenities                         3818 non-null   object        
 56  square_feet                       97 non-null     float64       
 57  price                             3818 non-null   int64         
 58  weekly_price                      2009 non-null   float64       
 59  monthly_price                     1517 non-null   float64       
 60  security_deposit                  1866 non-null   float64       
 61  cleaning_fee                      2788 non-null   float64       
 62  guests_included                   3818 non-null   int64         
 63  extra_people                      3818 non-null   int64         
 64  minimum_nights                    3818 non-null   int64         
 65  maximum_nights                    3818 non-null   int64         
 66  calendar_updated                  3818 non-null   object        
 67  has_availability                  3818 non-null   object        
 68  availability_30                   3818 non-null   int64         
 69  availability_60                   3818 non-null   int64         
 70  availability_90                   3818 non-null   int64         
 71  availability_365                  3818 non-null   int64         
 72  calendar_last_scraped             3818 non-null   datetime64[ns]
 73  number_of_reviews                 3818 non-null   int64         
 74  first_review                      3191 non-null   datetime64[ns]
 75  last_review                       3191 non-null   datetime64[ns]
 76  review_scores_rating              3171 non-null   float64       
 77  review_scores_accuracy            3160 non-null   float64       
 78  review_scores_cleanliness         3165 non-null   float64       
 79  review_scores_checkin             3160 non-null   float64       
 80  review_scores_communication       3167 non-null   float64       
 81  review_scores_location            3163 non-null   float64       
 82  review_scores_value               3162 non-null   float64       
 83  requires_license                  3818 non-null   object        
 84  license                           0 non-null      float64       
 85  jurisdiction_names                3818 non-null   object        
 86  instant_bookable                  3818 non-null   object        
 87  cancellation_policy               3818 non-null   object        
 88  require_guest_profile_picture     3818 non-null   object        
 89  require_guest_phone_verification  3818 non-null   object        
 90  calculated_host_listings_count    3818 non-null   int64         
 91  reviews_per_month                 3191 non-null   float64       
dtypes: datetime64[ns](5), float64(23), int64(15), object(49)
memory usage: 2.7+ MB

```
There are a total of 91 columns, but we don't need all of them. For example, the picture below shows some columns that contain long description contents, which we will not use.
<img width="1470" alt="code" src="https://github.com/cwnstae/cwnstae.github.io/blob/main/assets/Pic-Listings-1.png">
