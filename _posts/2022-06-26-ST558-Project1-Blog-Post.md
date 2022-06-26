Project 1 Reflection
================
Josh Baber
6/26/2022

## Links to GitHub repo and page

Link to GitHub page: <https://jababer.github.io/ST558Project/>

Link to GitHub repo: <https://github.com/JABaber/ST558Project>

## Summary of Project

In this first project for ST558, we mainly focused on pulling data from
an API, parsing it into neat and usable data, then created some tables
and graphs to analyze it. I chose to work with
[pokeAPI](%22https://pokeapi.co/%22), since I have way beyond a socially
acceptable amount of knowledge about Pokemon. Pokemon was a huge part of
my childhood growing up, and I continue to play the video games
occasionally even today. I decided to pull data from three endpoints
from the pokeAPI. One containing information about berries:
“<https://pokeapi.co/api/v2/berry/>” and two containing information
about Pokemon: <https://pokeapi.co/api/v2/pokemon/> and
<https://pokeapi.co/api/v2/pokemon-species/> . I then had to figure out
how to combine information from the two Pokemon endpoints, by Pokemon,
into one. After that, I parsed the data from the endpoints and converted
it to tibbles. Then I made a wrapper function called `queryAPI()` that
essentially contained all of the functions I had, so that the user can
query any combination of up to 19 predetermined Pokemon variables or any
variable from the berry endpoint. Using my `queryAPI()` function, I made
two large data sets, one about Pokemon and the other about berries, and
performed some analysis on them. My analysis included one-way and
two-way contingency tables, numerical summaries, often grouped by a
categorical variables, and graph, which also contained grouping or
coloring by a categorical variable.

## Interesting Findings

Some of the more interesting findings were in my contingency tables. For
example, I knew that water was the most common type, and dragon types
are typically the rarest, but it was interesting to see the exact
numbers of each type all in one place. The same thing goes for the fire
types table, where I looked to see if generation 4 really was abnormally
low on fire types. Generation 4 did indeed have the lowest amount of
fire types, but only by a margin of 1. Generation 3 had only 1 more fire
type Pokemon, but no one ever really gives it flack for that. The most
interesting summary to me was the catch rates, grouped by whether or not
Pokemon were legendary. The mean catch rate for legendaries was much,
much lower than the average catch rate for non-legendaries. I was not
expecting there to be such a huge difference, since many non-legendaries
are hard to catch too. Out of the graphs, I would have to say that the
first plot is the most interesting. It is a plot of attack against
special attack, colored by type 1. I expected to see many more psychic
types on the extreme ends of the “high special attack, low attack”
portion of the graph, and many normal and fighting types on the “high
attack, low special attack”. Overall, the distribution seemed a little
more even to me than I expected, and I was also surprised to see so many
Pokemon with equal special attack and attack.

## Difficulties and Future Prospects

This project took me a considerable amount of time. I would say my R
skills are passable at worst, but parsing some of this data, especially
when looping through many iterations, was a big pain. It would not have
been so bad if the data was returned as data frames, but have it
returned as a lists that contains 45 different variables comprised as
values, lists, lists within lists, data frames, and data frames within
lists made it pretty hard to keep track of everything. In the future, I
would probably try to make an effort to parse some of the data I wanted
earlier, before trying to convert everything into a tibble at once.
While many of the data points I threw out regarding Pokemon were useless
or irrelevant to statistical analysis, I still would like to see what I
can do with them. It may have also been easier to create tibbles for
each Pokemon endpoint, then combine them by id number or name in a join.
Regardless, the way I did it worked out okay, and the EDA part of it for
me was pretty straightforward. I will likely continue to work on this in
the future in my own time and see what interesting things I can find
with the data. I found GitHub to be a little bit unituitive to use at
first, especially with images, but once it got rolling it was great.
Overall, I enjoyed this project greatly and thought it was really cool
how easy it is to pull data from an API and analyze it.
