
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

# Lab Report \#2: Exploring Residential Sales in Ames

## Description

This lab explores residential sales data in Ames since 2017. Our team
analyzed various aspects of the dataset, including key variables
influencing sale prices. Findings are summarized below.

## Step 1 Result: Initial Data Inspection

- Identified dataset variables and their types
- Assessed expected data ranges
- Special focus variable selected for further exploration

``` r
load("ames.rda")
head(ames)
```

    ## # A tibble: 6 × 16
    ##   `Parcel ID` Address      Style Occupancy `Sale Date` `Sale Price` `Multi Sale`
    ##   <chr>       <chr>        <fct> <fct>     <date>             <dbl> <chr>       
    ## 1 0903202160  1024 RIDGEW… 1 1/… Single-F… 2022-08-12        181900 <NA>        
    ## 2 0907428215  4503 TWAIN … 1 St… Condomin… 2022-08-04        127100 <NA>        
    ## 3 0909428070  2030 MCCART… 1 St… Single-F… 2022-08-15             0 <NA>        
    ## 4 0923203160  3404 EMERAL… 1 St… Townhouse 2022-08-09        245000 <NA>        
    ## 5 0520440010  4507 EVERES… <NA>  <NA>      2022-08-03        449664 <NA>        
    ## 6 0907275030  4512 HEMING… 2 St… Single-F… 2022-08-16        368000 <NA>        
    ## # ℹ 9 more variables: YearBuilt <dbl>, Acres <dbl>,
    ## #   `TotalLivingArea (sf)` <dbl>, Bedrooms <dbl>,
    ## #   `FinishedBsmtArea (sf)` <dbl>, `LotArea(sf)` <dbl>, AC <chr>,
    ## #   FirePlace <chr>, Neighborhood <fct>

**What variables are there?**

- Parcel ID

- Address

- Style

- Occupancy

- Sale Date

- Sale Price

- Multi Sale

- YearBuilt

- Acres

- TotalLivingArea (sf)

- Bedrooms

- FinishedBsmtArea (sf)

- LotArea (sf)

- AC

- FirePlace

- Neighborhood

**Of what type are the variables?**

- Parcel ID: Character

- Address: Character

- Style: Factor

- Occupancy: Factor

- Sale Date: Date

- Sale Price: Double

- Multi Sale: Character

- YearBuilt: Double

- Acres: Double

- TotalLivingArea: Double

- Bedrooms: Double

- FinishedBsmtArea: Double

- LotArea: Double

- AC: Character

- FirePlace: Character

- Neighborhood: Factor

**What does each variable mean?**

- Parcel ID: Unique ID for each property

- Address: Street address of the property

- Style: Architectural style of the property

- Occupancy: If the property is owner occupied, tenant occupied, or
  vacant

- Sale Date: The date of when the property was sold

- Sale Price: How much the property was sold for

- Multi Sale: If the property was part of a multiple property
  transaction

- YearBuilt: The year the property was built

- Acres: Size of the property in acres

- TotalLivingArea (sf): Total livable area of the property in square
  feet

- Bedrooms: Number of bedrooms at the property

- FinishedBsmtArea (sf): Area of the finished basement in square feet

- LotArea (sf): Total area of the lot in square feet

- AC: If the property has air conditioning

- FirePlace: If the property has a fire place

- Neighborhood: Neighborhood where the property is located

## Step 2 Result: Exploration of Main Variable (Sale Price)

- Visualized the distribution of sale prices using histograms
- Noted general patterns and any anomalies
- Identified potential outliers

## Step 3 Result: Investigation of a Related Variable

- Selected a variable correlated with Sale Price (e.g., Lot Size, Year
  Built)
- Visualized the relationship with scatterplots and boxplots
- Analyzed patterns and identified any oddities

(Kush’s Work): A code chunk that creates a bar chart to display the
distribution of the number of bedrooms:

``` markdown
### Distribution of Bedrooms

Let's visualize the distribution of bedrooms across the properties:


``` r
# Plot the distribution of Bedrooms
ggplot(ames, aes(x = Bedrooms)) +
  geom_bar(fill = "lightgreen", color = "black") +
  labs(title = "Distribution of Bedrooms",
       x = "Number of Bedrooms",
       y = "Count") +
  theme_minimal()
```

![](README_files/figure-gfm/bedrooms-distribution-1.png)<!-- -->

Relationship between Bedrooms and Sale Price:

``` r
# Boxplot to show relationship between Bedrooms and Sale Price
ggplot(ames, aes(x = as.factor(Bedrooms), y = `Sale Price`)) +
  geom_boxplot(fill = "lightblue") +
  labs(title = "Sale Price by Number of Bedrooms",
       x = "Number of Bedrooms",
       y = "Sale Price ($)") +
  theme_minimal()
```

![](README_files/figure-gfm/bedrooms-saleprice-1.png)<!-- -->

## Step 4 Result: Team Member Contributions

- Ash’s work: Analyzed the effect of Lot Size on Sale Price, Examined
  the impact of Year Built on Sale Price and Investigated additional
  factors (e.g., Neighborhood, House Quality)

- Aden’s work: Analyzing the effect of Total Living Area on Sale Price.

``` r
ggplot(ames, aes(x = `TotalLivingArea (sf)`)) +
  geom_histogram(binwidth = 250, fill = "skyblue", color = "black") +
  labs(title = "Distribution of Total Living Area",
       x = "Total Living Area (sq ft)",
       y = "Count") +
  theme_minimal()
```

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

The plot is right skewed and we can see that our range is from somewhere
close to 0 sqft to 6000 sqft. Also, most homes have around 1500 - 2500
sqft.

``` r
ggplot(ames, aes(x = `TotalLivingArea (sf)`, y = `Sale Price`)) +
  geom_point(alpha = 0.6, color = "blue", size = 1.5) +  # Improved point visibility
  scale_y_continuous(limits = c(0, 2000000)) +  # Limit Sale Price to $2M to remove outliers
  labs(title = "Scatter Plot of Sale Price vs. Total Living Area",
       x = "Total Living Area (sqft)",
       y = "Sale Price ($)") +
  theme_minimal()
```

    ## Warning: Removed 779 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

As the Total Living Area increases Sale Price also tends to increase.
This makes sense as larger living spaces usually cost more.

- Kush’s work: Exploring the Impact of Bedrooms on Sale Price

In this section, I analyze how the number of bedrooms in a property
relates to its sale price. My hypothesis is that properties with an
optimal number of bedrooms (for example, 3–4 bedrooms) tend to have
higher sale prices compared to those with too few or too many bedrooms.

``` r
# Summary statistics for the Bedrooms variable
summary(ames$Bedrooms)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   0.000   3.000   3.000   3.299   4.000  10.000     447

``` r
# Plot the distribution of Bedrooms
ggplot(ames, aes(x = Bedrooms)) + 
  geom_bar(fill = "lightgreen", color = "black") + 
  labs(title = "Summary of Bedrooms", 
       x = "Number of Bedrooms", 
       y = "Count") + 
  theme_minimal()
```

![](README_files/figure-gfm/bedrooms-plot-1.png)<!-- -->

Distribution of Bedrooms: The bar chart shows that most properties in
the dataset have between 2 to 4 bedrooms, with 3-bedroom homes being the
most common. There are very few properties with 0, 7, 8, 9, or 10
bedrooms, indicating that such configurations are rare in this dataset.
A warning in the output suggests that 447 rows contained missing or
non-finite values, meaning there may be some properties without recorded
bedroom counts.

Sale Price vs. Number of Bedrooms The boxplot suggests that sale price
does not increase linearly with the number of bedrooms. While 1-bedroom
homes show a wide range of sale prices, including some extreme outliers,
properties with 2 to 5 bedrooms generally have more stable and lower
sale prices. Some extreme high-value outliers are present in the
dataset, particularly for 1-bedroom homes. The sale prices for homes
with 6 or more bedrooms remain relatively low, indicating that having a
very high bedroom count does not necessarily translate to higher
property value. Some properties are recorded as having 0 bedrooms, which
could be an error or represent non-residential buildings.

- Selim’s Work (Year Built and Sale Price Analysis) Observations: -The
  histogram shows that most homes were built in clusters, with spikes in
  certain decades. -There are some older homes with very high prices,
  likely due to renovations or historical significance. -Some newer
  homes sell for less than expected, possibly due to smaller size or
  location factors.

``` r
# Install missing packages
if (!require(dplyr)) install.packages("dplyr", dependencies=TRUE)
if (!require(ggplot2)) install.packages("ggplot2", dependencies=TRUE)

# Load libraries
library(dplyr)
library(ggplot2)

# Load the dataset
load("ames.rda")

# Check column names to verify correct Sale Price column name
print(colnames(ames))
```

    ##  [1] "Parcel ID"             "Address"               "Style"                
    ##  [4] "Occupancy"             "Sale Date"             "Sale Price"           
    ##  [7] "Multi Sale"            "YearBuilt"             "Acres"                
    ## [10] "TotalLivingArea (sf)"  "Bedrooms"              "FinishedBsmtArea (sf)"
    ## [13] "LotArea(sf)"           "AC"                    "FirePlace"            
    ## [16] "Neighborhood"

``` r
# Plot 1: Histogram of Year Built
ggplot(ames, aes(x = YearBuilt)) +
  geom_histogram(binwidth = 5, fill = "purple", color = "black") +
  labs(title = "Distribution of Year Built for Homes",
       x = "Year Built",
       y = "Count") +
  theme_minimal()
```

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-gfm/yearbuilt%20and%20sale-1.png)<!-- -->

## Summary of Findings

- Sale Price is significantly influenced by Lot Size and Year Built
- Certain neighborhoods show higher property values
- Anomalies and outliers identified in older properties and extreme lot
  sizes

## Conclusion

Our analysis provided insights into key factors affecting residential
property sales in Ames. Future work could include deeper statistical
modeling to refine predictions.
