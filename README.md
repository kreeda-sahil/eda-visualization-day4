# eda-visualization-day4

# Zomato Cleaning and Exploratory Data Analysis

This project cleans and explores a Zomato restaurant dataset using pandas, NumPy, Matplotlib, and Seaborn. The notebook produces a modeling-ready dataset and investigates restaurant ratings, pricing, location, cuisine, service options, and restaurant formats.

## Dataset

- Input: `zomato.csv`
- Output: `zomato_cleaned.csv`
- Output size: 51,717 rows and 23 columns
- Main target explored: `rate`, the restaurant rating out of 5

## Data Cleaning

The notebook performs the following preparation steps:

1. Removes high-cardinality or unused text fields: `url`, `phone`, `menu_item`, `address`, and `reviews_list`.
2. Renames columns containing spaces or punctuation to clearer names such as `approx_cost_for_two`, `listing_type`, `listed_city`, and `restaurant_type`.
3. Cleans `rate` by removing spaces and `/5`, converts `NEW` and `-` to missing values, and casts the column to `float`.
4. Removes commas from `approx_cost_for_two` and converts it to a numeric column.
5. Fills missing costs with the median cost for the restaurant type, followed by the overall median when required.
6. Replaces missing restaurant types, cuisines, and locations with `Unknown`.
7. Encodes `online_order` and `book_table` from `Yes`/`No` to `1`/`0`.

## Feature Engineering

The notebook adds features for analysis and future machine-learning work:

- `cuisine_count`: number of cuisines listed for a restaurant
- `primary_cuisine`: first cuisine in the cuisine list
- `dish_liked_count`: number of dishes listed in `dish_liked`
- `has_dish_liked`: indicator for whether liked-dish information exists
- `primary_restaurant_type`: first restaurant type in the type list
- `cost_bucket`: Budget, Mid-Range, Premium, or Luxury based on approximate cost for two
- `votes_log`: `log1p(votes)` to reduce the effect of the highly skewed vote counts
- `is_chain`: indicator for restaurant names appearing in more than one location
- `location_avg_rating`: mean rating for the restaurant's location
- `location_density`: number of listings in the restaurant's location

## Exploratory Analysis

The notebook visualizes and compares:

- Distributions and skewness of ratings, cost, and votes
- Online ordering and table-booking availability
- Restaurant listing types, restaurant formats, and the top primary cuisines
- True restaurant hotspots after removing repeated `name` and `location` records
- Correlations among rating, votes, cost, cuisine count, online ordering, and table booking
- Rating differences by cost bucket, online-order availability, table-booking availability, listing type, cuisine count, and location
- Relationships between rating and cost, and between rating and raw or log-transformed votes
- Potential outliers in cost and votes using box plots and the IQR method

## Main Takeaways

The analysis shows that the dataset is highly heterogeneous: restaurants vary considerably in cost, popularity, cuisine coverage, service model, and location. Vote counts and cost are strongly right-skewed, which motivates the log transformation for votes and the use of medians and box plots when comparing groups. Location and restaurant identity also require care because one restaurant can appear in multiple locations or listings; therefore, the notebook uses unique `name`-`location` pairs for physical-restaurant counts.

The correlation and group comparisons are descriptive rather than causal. A difference in ratings between price tiers or service categories does not by itself show that the category causes a higher rating.

