Coolest Thing I’ve Learned in R
================
Josh Baber
6/28/2022

# ST558 Third Blog Post

## Getting Data From APIs

By far the coolest thing I’ve learned so far with R is how to interact
with APIs. Before this course, I did not even know what an API was, but
now I see how useful they can be, especially when used with a
statistical programming software like R. It’s super easy and fast to
grab just about any custom data or information that we want, and then we
can use R to perform statistical analyses with graphs, tables, and
summaries on that data.

## A Quick Example of Using an API

Some APIs require keys, but this [pokeAPI](https://pokeapi.co/) does
not. Using the `fromJSON()` function from the `jsonlite` package, we can
easily pull data from a URL that we get by reading the docs of the API.
In this example, I can pull a ton of information about the move
“Thunder” and print out its accuracy, power, and type.

``` r
# Read in jsonlite
library(jsonlite)
# Grab information about the move thunder
thunder <- fromJSON("https://pokeapi.co/api/v2/move/thunder")
# Print out thunder's accuracy, power, and type
c(thunder$accuracy, thunder$power, thunder$type$name)
```

    ## [1] "70"       "110"     
    ## [3] "electric"
