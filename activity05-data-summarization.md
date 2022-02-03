Activity 5
================
Nathan Vandermeer

## Data and packages

Again, we will load all of the `{tidyverse}` for this Activity.

``` r
library(tidyverse)
```

We continue our exploration of college majors and earnings from the data
behind the FiveThirtyEight story [The Economic Guide To Picking A
College
Major](https://fivethirtyeight.com/features/the-economic-guide-to-picking-a-college-major/).
Remember that there are many considerations that go into picking a
major. Earning potential and employment prospects are two (important) of
these considerations, but they do not tell the entire story.

We read in the same data from Activity 4 below, but notice that this
code is now surrounded in parentheses.

``` r
(college_recent_grads <- read_csv("data/recent-grads.csv"))
```

    ## # A tibble: 173 x 21
    ##     rank major_code major           major_category total sample_size   men women
    ##    <dbl>      <dbl> <chr>           <chr>          <dbl>       <dbl> <dbl> <dbl>
    ##  1     1       2419 Petroleum Engi… Engineering     2339          36  2057   282
    ##  2     2       2416 Mining And Min… Engineering      756           7   679    77
    ##  3     3       2415 Metallurgical … Engineering      856           3   725   131
    ##  4     4       2417 Naval Architec… Engineering     1258          16  1123   135
    ##  5     5       2405 Chemical Engin… Engineering    32260         289 21239 11021
    ##  6     6       2418 Nuclear Engine… Engineering     2573          17  2200   373
    ##  7     7       6202 Actuarial Scie… Business        3777          51  2110  1667
    ##  8     8       5001 Astronomy And … Physical Scie…  1792          10   832   960
    ##  9     9       2414 Mechanical Eng… Engineering    91227        1029 80320 10907
    ## 10    10       2408 Electrical Eng… Engineering    81527         631 65511 16016
    ## # … with 163 more rows, and 13 more variables: sharewomen <dbl>,
    ## #   employed <dbl>, employed_fulltime <dbl>, employed_parttime <dbl>,
    ## #   employed_fulltime_yearround <dbl>, unemployed <dbl>,
    ## #   unemployment_rate <dbl>, p25th <dbl>, median <dbl>, p75th <dbl>,
    ## #   college_jobs <dbl>, non_college_jobs <dbl>, low_wage_jobs <dbl>

Compare this code output to the `load_data` chunk in your knitted
Activity 4 `.md` report. What does enclosing an assignment code (i.e.,
`object_name <- r_code`) in parentheses do?

**Response**: Shows the output for that variable

### Data Codebook

Descriptions of the variables are again provided below. Again note that
the ACS only asks [one
question](https://www.census.gov/acs/www/about/why-we-ask-each-question/sex/)
about a person’s sexual identity.

| Header                         | Description                                                                 |
|:-------------------------------|:----------------------------------------------------------------------------|
| `rank`                         | Rank by median earnings                                                     |
| `major_code`                   | Major code, FO1DP in ACS PUMS                                               |
| `major`                        | Major description                                                           |
| `major_category`               | Category of major from Carnevale et al                                      |
| `total`                        | Total number of people with major                                           |
| `sample_size`                  | Sample size (unweighted) of full-time, year-round ONLY (used for earnings)  |
| `men`                          | Male graduates                                                              |
| `women`                        | Female graduates                                                            |
| `sharewomen`                   | Women as share of total                                                     |
| `employed`                     | Number employed (ESR == 1 or 2)                                             |
| `employed_full_time`           | Employed 35 hours or more                                                   |
| `employed_part_time`           | Employed less than 35 hours                                                 |
| `employed_full_time_yearround` | Employed at least 50 weeks (WKW == 1) and at least 35 hours (WKHP &gt;= 35) |
| `unemployed`                   | Number unemployed (ESR == 3)                                                |
| `unemployment_rate`            | Unemployed / (Unemployed + Employed)                                        |
| `median`                       | Median earnings of full-time, year-round workers                            |
| `p25th`                        | 25th percentile of earnings                                                 |
| `p75th`                        | 75th percentile of earnings                                                 |
| `college_jobs`                 | Number with job requiring a college degree                                  |
| `non_college_jobs`             | Number with job not requiring a college degree                              |
| `low_wage_jobs`                | Number in low-wage service jobs                                             |

The questions we will answer in this activity are:

-   How do the distributions of median income compare across major
    categories?
-   Do women tend to choose majors with lower or higher earnings?

## Analysis

### Median Earnings Description

### Median … Median Earnings

For the rest of this semester, I will no longer provide you with R code
chunks. Have no fear! There are a number of ways to create a code chunk:

-   Tired: Copy-and-paste a previous code chunk, delete the code, then
    add your new code
-   Wired: Click on the ![new chunk icon](README-img/new-chunk-icon.png)
    and select ![r chunk icon](README-img/r-chunk-icon.png) (notice all
    the different types of code chunks that you can use within an
    RMarkdown file!)
-   Inspired: Ctrl/Command + Alt/Option + I

Below, create a code chunk and name it `median_earnings`. Make sure
there is an empty line above and below the code chunk.

``` r
college_recent_grads %>%
  summarise(median(median))
```

    ## # A tibble: 1 x 1
    ##   `median(median)`
    ##              <dbl>
    ## 1            36000

In your newly created R code chunk, verify that the median income for
all majors was $36,000. Using the `college_recent_grads` dataset and
functions from `{dplyr}`, verify the *median* summary statistic for the
variable median earnings of full-time, year-round workers (`median`).
Name this numerical summary `median_all_majors`.

![](README-img/noun_pause.png) **Planned Pause Point**: If you have any
questions, contact your instructor. Otherwise feel free to continue on.

### Additional Summaries of Median Earnings

Often we would like more information than the median to help us to
better understand the distribution of a variable. Using the
`college_recent_grads` dataset and functions from `{dplyr}`, obtain the
sample size (i.e., *n*umber of observations), *mean*, *s*tandard
*d*eviation, *min*imum, *median*, and *max*imum summaries for the
variable `median` earnings of full-time, year-round workers. Be careful
when you name your output summaries as we are dealing with things that
could use the same name (i.e., “median”). When I and obtaining numerical
summaries for variables, I like to include the variable name in my
summary name (e.g., `mean_med_earnings = mean(median)`). Create a code
chunk and name it `summary_earnings`.

``` r
college_recent_grads %>%
  summarise(n=n(),mean_med_earnins=mean(median),st_dev=sd(median),min=min(median),median=median(median),max=max(median))
```

    ## # A tibble: 1 x 6
    ##       n mean_med_earnins st_dev   min median   max
    ##   <int>            <dbl>  <dbl> <dbl>  <dbl> <dbl>
    ## 1   173           40151. 11470. 22000  36000 36000

Provide a discussion on what you believe the distribution of median
earnings will look like. You should discuss the center, spread, and
potential shape only using these values - I do NOT want to see any data
visualizations here.

**Response**: Because the mean is greater than the median, I expect the
shape to be skewed right.

### Median Earnings by Major Category

Now we will see how the different major categories compare to the
overall distribution of median earnings. Using the
`college_recent_grads` dataset and functions from `{dplyr}`, obtain
similar summaries of the variable `median` earnings of full-time,
year-round workers as your `summary_earnings` code chunk, *by* for each
`major_category`. *Arrange* this summary table by the median earning.
Create a code chunk and name it `major_earnings`.

``` r
college_recent_grads %>% 
  group_by(major_category) %>% 
  summarise(n=n(),mean=mean(employed_fulltime_yearround),st_dev=sd(employed_fulltime_yearround),min=min(employed_fulltime_yearround),median=median(employed_fulltime_yearround),max=max(employed_fulltime_yearround)) %>% 
  knitr::kable()
```

| major\_category                     |   n |      mean |   st\_dev |   min |  median |    max |
|:------------------------------------|----:|----------:|----------:|------:|--------:|-------:|
| Agriculture & Natural Resources     |  10 |  4362.600 |  3688.871 |   383 |  3142.5 |  10824 |
| Arts                                |   8 | 19138.875 | 16490.457 |  1200 | 16315.5 |  52243 |
| Biology & Life Science              |  14 | 11843.000 | 25748.885 |   565 |  4811.0 | 100336 |
| Business                            |  13 | 60801.923 | 68023.475 |  2482 | 15446.0 | 199897 |
| Communications & Journalism         |   4 | 53557.000 | 42099.987 | 27521 | 35228.0 | 116251 |
| Computers & Mathematics             |  11 | 14468.727 | 21239.676 |   391 |  4936.0 |  70932 |
| Education                           |  16 | 18001.938 | 25107.980 |   410 |  9032.0 |  86540 |
| Engineering                         |  29 |  9963.862 | 13932.153 |   340 |  3413.0 |  54639 |
| Health                              |  12 | 19034.833 | 33069.638 |  3236 |  9068.0 | 122817 |
| Humanities & Liberal Arts           |  15 | 19704.067 | 22522.806 |  1274 | 13109.0 |  81180 |
| Industrial Arts & Consumer Services |   7 | 16311.286 | 20400.761 |   111 |  9170.0 |  57978 |
| Interdisciplinary                   |   1 |  6234.000 |        NA |  6234 |  6234.0 |   6234 |
| Law & Public Policy                 |   5 | 20090.800 | 38302.928 |   808 |  2952.0 |  88548 |
| Physical Sciences                   |  10 |  8563.500 | 11752.139 |   653 |  1878.0 |  29910 |
| Psychology & Social Work            |   9 | 24233.889 | 56962.077 |   529 |  2738.0 | 174438 |
| Social Science                      |   9 | 28357.667 | 32251.211 |  1530 | 10548.0 |  83236 |

Provide a discussion on how each major compares to the overall
distribution. You should discuss the center, spread, and potential shape
only using these summary values - I do NOT want to see any data
visualizations here.

**Response**: Business, Communications & Journalism are the only majors
that have a higher mean of the median. Also, for every major, the mean
is greater than the median. So, just as with the total of all majors, we
can expect them to be right skewed.

Before we continue, add the following to the end of your pipeline (you
will need to pipe first) in your `major_earnings` code chunk:

    knitr::kable()

Knit your document with and without this last piped code. What changes
about the output? When would this `knitr::kable` code be useful?

**Response**: Makes the data frame into a nice table

![](README-img/noun_pause.png) **Planned Pause Point**: If you have any
questions, contact your instructor. Otherwise feel free to continue on.

### Visualize Median Earnings by Major Category

Let us see how well your descriptions in the [Median Earnings by Major
Category](#median-earnings-by-major-category) section compare to the
actual distributions. Plot the distribution of the variable `median`
earnings of full-time, year-round workers for each `major_category`
using the *boxplot* and *jitter* geometries. Create a code chunk and
name it `major_boxplot`.

``` r
ggplot(data=college_recent_grads, aes(x=major_category,y=median))+
  geom_boxplot()+
  geom_jitter()
```

![](activity05-data-summarization_files/figure-gfm/major_boxplot-1.png)<!-- -->

Provide a discussion on how your descriptions in the Median Earnings by
Major Category section compares.

**Response**: So this graph is really messy, but it does appear that
some of the Major Categories are right skewed, however, there also
appear to be some left skewed ones.

<img src="README-img/noun_pause.png" alt="pause" width = "20"/>
<b>Planned Pause Point</b>: If you feel that you have a good
understanding of these commands, feel free to start working on your
project. The remainder of this activity will help to expand these
commands.

### Multiple Rankings

#### Ranking by `major_category`

The current rankings provided in the data are by `major`. Here we will
develop a series of rankings to see how the `major_category` levels
perform. Create a code chunk and name it `category_rankings`. In this
code chunk,

1.  Group `college_recent_grads` by `major_category`
2.  Summarize the variable `total` as the *sum* across all majors (to
    get the total number of majors within a `major_category`) and the
    following variables by their *median* value: `sharewomen`,
    `unemployment_rate`, and `median` earnings. Provide a meaningful
    name to each summarized value.
3.  Assign/create a *rank* for each summarized value (rank for `total`,
    rank for `sharewomen`, etc.) and provide a meaningful name to each
    ranked column value.
4.  Arrange the results so that `major_category` appear in alphabetical
    order (“A” at the top).

``` r
college_recent_grads %>% 
  group_by(major_category) %>% 
  summarise(total_sum=sum(total),med_sharewomen=median(sharewomen), med_unemploy=median(unemployment_rate), med_median=median(median)) %>% 
  mutate(ranked_total=min_rank(total_sum),ranked_sharewomen=min_rank(med_sharewomen),ranked_unemployment=min_rank(med_unemploy),ranked_median=min_rank(med_median)) %>% 
  arrange(major_category) %>% 
  select(major_category,ranked_total,ranked_sharewomen,ranked_unemployment,ranked_median)
```

    ## # A tibble: 16 x 5
    ##    major_category   ranked_total ranked_sharewom… ranked_unemploy… ranked_median
    ##    <chr>                   <int>            <int>            <int>         <int>
    ##  1 Agriculture & N…           NA               NA                3             5
    ##  2 Arts                        6                9               14             2
    ##  3 Biology & Life …            8                8                8            11
    ##  4 Business                   15                4                9            14
    ##  5 Communications …            7               10               11             5
    ##  6 Computers & Mat…            5                3               15            15
    ##  7 Education                  13               12                1             4
    ##  8 Engineering                12                1                5            16
    ##  9 Health                      9               14                6             5
    ## 10 Humanities & Li…           14               11               12             3
    ## 11 Industrial Arts…            4                2                4             5
    ## 12 Interdisciplina…            1               13               10             5
    ## 13 Law & Public Po…            2                5               13            10
    ## 14 Physical Scienc…            3                6                2            13
    ## 15 Psychology & So…           10               15                7             1
    ## 16 Social Science             11                7               16            12

Provide a discussion on how the `major_category` rankings compare.

**Response**: The Major with the lowest share of women is engineering,
and it also has some of the highest pay. Conversely, Psychology has the
highest share of women, and has the lowest median pay.

![](README-img/noun_pause.png) **(Final) Planned Pause Point**: If you
have any questions, contact your instructor. Otherwise feel free to
continue on.

Knit, then stage everything listed in your **Git** pane, commit (with a
meaningful commit message), and push to your GitHub repo. Go to GitHub
and verify that your `activity04-data-pieplines.Rmd` file appears as you
intended it to.

You can now go back to the `README` file.

## Attribution

This activity is inspired by a lab from [Dr. Mine
Çetinkaya-Rundel](http://www2.stat.duke.edu/~mc301/)’s STA 199 course.
