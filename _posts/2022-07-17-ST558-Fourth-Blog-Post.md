Machine Learning Methods
================
Josh Baber
7/17/2022

<https://www.kaggle.com/datasets/pushprajnamdev/diabetes-dataset>

``` r
library(tidyverse)
diabetes <- read_csv("../../Data/diabetes.csv")
```

    ## Rows: 768 Columns: 9
    ## ── Column specification ───────────────────────────────────
    ## Delimiter: ","
    ## dbl (8): pregnancies, glucose, bloodpressure, skinthick...
    ## lgl (1): outcome
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
