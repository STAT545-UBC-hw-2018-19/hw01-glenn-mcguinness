STAT 545A - Homework 1 Gapminder Exploration
================

-   [Introduction](#introduction)
-   [Gapminder Exploration](#gapminder-exploration)
    -   [Overview and Summary Statistics](#overview-and-summary-statistics)
    -   [Overview of Oceania](#overview-of-oceania)
-   [Conclusion](#conclusion)

Introduction
------------

In this document I will be performing a brief exploration of the gapminder dataset, while using some R markdown features.

Gapminder Exploration
---------------------

### Overview and Summary Statistics

First, I will install the dataset.

``` r
library(gapminder)
```

Now, I will check the size. If it is small enough, I will look at the contents of the data frame.

``` r
print(colnames(gapminder))
```

    ## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"

``` r
print(nrow((gapminder)))
```

    ## [1] 1704

I can not reasonable print 'r nrow(gapminder)' columns, so I will instead look at some interesting subsets of the data. First, I will get an idea of the structure.

``` r
# Here, we will take a look at different subsets of the table
# This is a handy way to get an idea of what the table contains
# The structure is less readable, but gives the precise types, which can be important.
# For example, knowing if a field is a double or an integer can be important.
head(gapminder)
```

    ## # A tibble: 6 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.
    ## 6 Afghanistan Asia       1977    38.4 14880372      786.

``` r
tail(gapminder)
```

    ## # A tibble: 6 x 6
    ##   country  continent  year lifeExp      pop gdpPercap
    ##   <fct>    <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Zimbabwe Africa     1982    60.4  7636524      789.
    ## 2 Zimbabwe Africa     1987    62.4  9216418      706.
    ## 3 Zimbabwe Africa     1992    60.4 10704340      693.
    ## 4 Zimbabwe Africa     1997    46.8 11404948      792.
    ## 5 Zimbabwe Africa     2002    40.0 11926563      672.
    ## 6 Zimbabwe Africa     2007    43.5 12311143      470.

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

Now we can get some summary statistics.

    ##         country        continent        year         lifeExp     
    ##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
    ##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
    ##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
    ##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
    ##  Australia  :  12                  Max.   :2007   Max.   :82.60  
    ##  (Other)    :1632                                                
    ##       pop              gdpPercap       
    ##  Min.   :6.001e+04   Min.   :   241.2  
    ##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
    ##  Median :7.024e+06   Median :  3531.8  
    ##  Mean   :2.960e+07   Mean   :  7215.3  
    ##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
    ##  Max.   :1.319e+09   Max.   :113523.1  
    ## 

Now, let's look at the summary statistics for each continent individually.

``` r
# We will iterate throught the different continents and print the summary
# It is not necessary to save this to a variable, but 
for (continent in unique(gapminder$continent))
{
  print(summary(gapminder[gapminder$continent == continent,]))
}
```

    ##              country       continent        year         lifeExp     
    ##  Afghanistan     : 12   Africa  :  0   Min.   :1952   Min.   :28.80  
    ##  Bahrain         : 12   Americas:  0   1st Qu.:1966   1st Qu.:51.43  
    ##  Bangladesh      : 12   Asia    :396   Median :1980   Median :61.79  
    ##  Cambodia        : 12   Europe  :  0   Mean   :1980   Mean   :60.06  
    ##  China           : 12   Oceania :  0   3rd Qu.:1993   3rd Qu.:69.51  
    ##  Hong Kong, China: 12                  Max.   :2007   Max.   :82.60  
    ##  (Other)         :324                                                
    ##       pop              gdpPercap     
    ##  Min.   :1.204e+05   Min.   :   331  
    ##  1st Qu.:3.844e+06   1st Qu.:  1057  
    ##  Median :1.453e+07   Median :  2647  
    ##  Mean   :7.704e+07   Mean   :  7902  
    ##  3rd Qu.:4.630e+07   3rd Qu.:  8549  
    ##  Max.   :1.319e+09   Max.   :113523  
    ##                                      
    ##                    country       continent        year     
    ##  Albania               : 12   Africa  :  0   Min.   :1952  
    ##  Austria               : 12   Americas:  0   1st Qu.:1966  
    ##  Belgium               : 12   Asia    :  0   Median :1980  
    ##  Bosnia and Herzegovina: 12   Europe  :360   Mean   :1980  
    ##  Bulgaria              : 12   Oceania :  0   3rd Qu.:1993  
    ##  Croatia               : 12                  Max.   :2007  
    ##  (Other)               :288                                
    ##     lifeExp           pop             gdpPercap      
    ##  Min.   :43.59   Min.   :  147962   Min.   :  973.5  
    ##  1st Qu.:69.57   1st Qu.: 4331500   1st Qu.: 7213.1  
    ##  Median :72.24   Median : 8551125   Median :12081.8  
    ##  Mean   :71.90   Mean   :17169765   Mean   :14469.5  
    ##  3rd Qu.:75.45   3rd Qu.:21802867   3rd Qu.:20461.4  
    ##  Max.   :81.76   Max.   :82400996   Max.   :49357.2  
    ##                                                      
    ##          country       continent        year         lifeExp     
    ##  Algeria     : 12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Angola      : 12   Americas:  0   1st Qu.:1966   1st Qu.:42.37  
    ##  Benin       : 12   Asia    :  0   Median :1980   Median :47.79  
    ##  Botswana    : 12   Europe  :  0   Mean   :1980   Mean   :48.87  
    ##  Burkina Faso: 12   Oceania :  0   3rd Qu.:1993   3rd Qu.:54.41  
    ##  Burundi     : 12                  Max.   :2007   Max.   :76.44  
    ##  (Other)     :552                                                
    ##       pop              gdpPercap      
    ##  Min.   :    60011   Min.   :  241.2  
    ##  1st Qu.:  1342075   1st Qu.:  761.2  
    ##  Median :  4579311   Median : 1192.1  
    ##  Mean   :  9916003   Mean   : 2193.8  
    ##  3rd Qu.: 10801490   3rd Qu.: 2377.4  
    ##  Max.   :135031164   Max.   :21951.2  
    ##                                       
    ##       country       continent        year         lifeExp     
    ##  Argentina: 12   Africa  :  0   Min.   :1952   Min.   :37.58  
    ##  Bolivia  : 12   Americas:300   1st Qu.:1966   1st Qu.:58.41  
    ##  Brazil   : 12   Asia    :  0   Median :1980   Median :67.05  
    ##  Canada   : 12   Europe  :  0   Mean   :1980   Mean   :64.66  
    ##  Chile    : 12   Oceania :  0   3rd Qu.:1993   3rd Qu.:71.70  
    ##  Colombia : 12                  Max.   :2007   Max.   :80.65  
    ##  (Other)  :228                                                
    ##       pop              gdpPercap    
    ##  Min.   :   662850   Min.   : 1202  
    ##  1st Qu.:  2962359   1st Qu.: 3428  
    ##  Median :  6227510   Median : 5466  
    ##  Mean   : 24504795   Mean   : 7136  
    ##  3rd Qu.: 18340309   3rd Qu.: 7830  
    ##  Max.   :301139947   Max.   :42952  
    ##                                     
    ##         country      continent       year         lifeExp     
    ##  Australia  :12   Africa  : 0   Min.   :1952   Min.   :69.12  
    ##  New Zealand:12   Americas: 0   1st Qu.:1966   1st Qu.:71.20  
    ##  Afghanistan: 0   Asia    : 0   Median :1980   Median :73.67  
    ##  Albania    : 0   Europe  : 0   Mean   :1980   Mean   :74.33  
    ##  Algeria    : 0   Oceania :24   3rd Qu.:1993   3rd Qu.:77.55  
    ##  Angola     : 0                 Max.   :2007   Max.   :81.23  
    ##  (Other)    : 0                                               
    ##       pop             gdpPercap    
    ##  Min.   : 1994794   Min.   :10040  
    ##  1st Qu.: 3199212   1st Qu.:14142  
    ##  Median : 6403492   Median :17983  
    ##  Mean   : 8874672   Mean   :18622  
    ##  3rd Qu.:14351625   3rd Qu.:22214  
    ##  Max.   :20434176   Max.   :34435  
    ## 

This provides some interesting results. The country with the lowest life expectancy is Rwanda in the year `gapminder$year[which.min(gapminder$lifeExp)]`. The country with the highest life expectancy is Japan in the year 2007.

### Overview of Oceania

Now, I will look at Oceania in particuar and take a look at some statistics for countries in Oceania.

The countries in Oceania are:

``` r
print(unique(gapminderOceania$country))
```

    ## [1] Australia   New Zealand
    ## 142 Levels: Afghanistan Albania Algeria Angola Argentina ... Zimbabwe

For the experience, I will calculate a simple statistic, manually. I will caluclate the sample variance of the life expectancy, using the formula
$$ S^2 = \\frac{1}{n-1} \\cdot \\sum\_{i=1}^{n} (X\_i - \\bar{X})^2$$
 and utilizing the vectorization feature of R.

``` r
print("Variance")
```

    ## [1] "Variance"

``` r
sum((gapminderOceania$lifeExp - mean(gapminderOceania$lifeExp))^2)
```

    ## [1] 331.3533

Conclusion
----------

In this document, we briefly reviewed the gapminder dataset provided by the gapminder library. We observed some summary stastics of the entire population and then some subsets of interest. This provided the opportunity to use some features of R markdown to provide a clear and re-usable view of the data.
