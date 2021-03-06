---
title: "An Introduction to Data Science with R"
author: "Richie Erickson, USGS and Nick Rasmussen, CA Department of Water Resources"
output:
  html_document:
    keep_md: yes
    toc: yes
  html_notebook:
    toc: yes
---

_Fundamentally learning about the world through data is really, really cool._ 
-- Hadley Wickham

_You too can be a toxicologist in two easy lessons, each of ten years._
-- Arnold Lehman 

## Course goals

Provide an introduction to R and tools for data manipulation and statistics in R. 
Specifically, focusing on newer R packages that have emerged over the past decade for "Data Science". 
Specific course outcomes include:

 - Using Scripts and R Markdown to create reproducible results. 
 - Learn about basic data manipulation with `Tidyverse`
 - Learn the basics of `ggplot2` for plotting
 - Learn the basics of date manipulation in R with `lubridate`
 - Briefly overview statistics and regression models in R 

These objectives will roughly follow Garrett Grolemund and Hadley Wickham's modeling process, which is described in their book, [R for Data Science.](http://r4ds.had.co.nz/):

![Worflow for data science described in [_R for Data Science_. ](http://r4ds.had.co.nz/)](http://r4ds.had.co.nz/diagrams/data-science-explore.png)

## FAQs

_What is data science?_

**Short answer:** 

A collection of approaches to help you deal with messy, large, or otherwise difficult to deal with data. 


**Long answer:** 

Data are messy.

Environmental and ecological data are no exception. 
Even laboratory generated data such as chemistry instrument outputs and toxicology studies can be difficult to work with. 
Data science provides tools to work with difficult and messy data.
Data science combines statistics with computer science to help people understand data and apply it to decision making.
Many applied statisticians and scientists have been data scientists without realizing it because they deal with these problems on a regular basis.
In fact, the tools developed by these people serve as the foundational tools used by data scientists. 

The most cynical definition I've read is that _data science_ was a term invented for PhD-level physicists who were sitting around running regression all day. 

_How is data science different from traditionaly statistcs?_

This question is up for debate. 
Many people would argue that it is not.
Others argue that data science includes more emphasis on computer science, making predictions, guiding decision making, and communicating results to non-technical audiences. 
Also, "data journalism" has emerged from data science with sites such as [FiveThirtyEight](http://fivethirtyeight.com/).

I would argue that many research scientists are already "data scientists" even if they did not know it.

_Why am I here or what will this course cover?_

I will cover some topics that I use for data science with R.
Specific topics include:

- Creating reproducible results using [R Markdown](http://rmarkdown.rstudio.com).
- Using the Tidyverse to manipulate data. Additionally, this will be contrasted with base R's functions. 
- Visualizing data using `ggplot2`.
- An overview of regression modeling in R. 

I will use RStudio for the course because it makes R Markdown file easy to use and so that you can follow along with this file.


_What is my experince with Data Science?_

I've been a "UseR" since 2007 when I started graduate school at Texas Tech.
After finishing my PhD in 2013, I started with the US Geological Survey where I often work with diverse and large datasets. 
Example datasets include:

- [Continental species distribution modeling that included wind turbine data](https://peerj.com/articles/2830/)
- [Telemetry data used to examine animal behavior](http://www.nrcresearchpress.com/doi/abs/10.1139/cjfas-2015-0472#.WunyadMvzc8)
- [Environmental DNA distributional data](https://onlinelibrary.wiley.com/doi/full/10.1111/1755-0998.12533)
- [Metabolimic data after toxicant exposure](https://www.sciencedirect.com/science/article/pii/S0045653516315818)
- [Tress swallow response to multiple endpoints](https://link.springer.com/article/10.1007/s10646-017-1863-7)
- [Tree swallow chromosomal damage](https://link.springer.com/article/10.1007/s10646-015-1443-7)

The tools in this course is based upon the tools I have used for these projects and others. 


_Why did you sign up for this course, or what data problems do you have?_

-
-
-

_How much prior exiernce do you have with R?_

_How much prior exiernce do with other stats programs/languages?_


## What is R and RStudio?

R is basically a giant calculator. 
If you open up R, you will see a terminal. 
Try typing commands like `2 + 2` or `sin(0)`. 
You can also save objects using the assign key `x <- 2` or equals sign `y = 3`.  

We can save our R outputs for later using script files. 
Watch along as I demonstrate script files. 
These allow you to save outputs for later. 


Notice, plain R is pretty basic. 
Hence, other programs exist such as RStudio that make R easier to use. 
Now, let's open up RStudio. 
Notice by default there are multiple panes. 
You can also customize the location of these panes. 
Other key points include:

- Help files
- Packages 
- New scripts 
- Working directory 

## Creating reproducilbe results

**Problem:** How do I document code so that others and myself can reproduce my results? 

**Solution:** Scripts and R Markdown!

Congratulations, you're using a file generated by R Markdown now!
This document is an R Notebook, a type of R Markdown file.
R Markdown is a flavor of Markdown designed to work with R.
It was created to overcome many of the shortcomings of `Sweave`, which "weaves" S (and also R) code into LaTeX documents.
More broadly, Markdown is a computer programming "shortcut" language that takes easier to write code and complies it to HTLM.

R Markdown allows the R language to be embedded in Markdown. 
This allows you to keep your code with a document for reproducible results. 
I have seen theses, dissertations, books, and journal articles written in Markdown. 
Also, R now allows documentation to be written in Markdown (e.g., [the vignettes for ggplot2](https://cran.r-project.org/web/packages/ggplot2/index.html)). 
Markdown also can help with "production" code that you run on a regular basis (e.g., weekly reports from chemistry instruments or statistical reports written for clients). 

Here is an example of embedded code to do things like show 2 + 2 is 4. 
Or, we can enter code into code blocks. 


```r
2 + +2 
```

```
## [1] 4
```

We can also embedded plots and not include the code in the plot:


```r
x <- 1:10
y <- exp(x)
plot(x,y)
```

![](Notebook_files/figure-html/unnamed-chunk-2-1.png)<!-- -->
Notice the use of `<-` to assign or save an object. 
We can also use `=`. 
Two methods exist due to historical nomenclature in R. 

Next, I will open up a new R Markdown file in R Studio to demonstrate how it can be used.
Key points include:

- Basic syntax
- Code "chunks"
- Including figures
- Cheat sheets builds into [RStudio](https://rmarkdown.rstudio.com/lesson-15.html)
- Tutorials from [RStuido](https://rmarkdown.rstudio.com/)

**Downside:** Advanced formatting requires understanding CSS files and LaTeX.

### Exercise

1. Open your own RMarkdown file and compile it.
2. Create headings and subheadings.

## Import data

### Today's data

For the first half of today, we will be using data from a project I'm part of at work. 
Environmental DNA (eDNA) copy numbers and adult sea lamprey Densities from a USGS-funded master's project.
The data is described [online](https://www.sciencebase.gov/catalog/item/59b6cc06e4b08b1644ddf8b3).
The main research question with this dataset was asking: Does lamprey stocking density correspond to the amount of eDNA? 

### Reading in data

When reading in data, open source files such as CSVs work best.
Most spreadsheet programs have a "save as" option that allows spreadsheeds to be exported as CSV files. 
As we will see today, these files do not need to be local. 
Instead, they can be downloaded directly from the webpage. 
Also, R had build in datasets for demonstrating packages and teaching. 
RStudio also has a point-and-click option, but I find this creates more long-term problems than it solves and is best avoided. 
For example, which version of a file did you load 5 months ago and where was that file located? 
Today, we'll go over multiple methods for loading data including base R and the Tidyverse. 

### Reading in data

Base R reads data files in and creates `data.frames`. 


```r
adults_df <- read.csv("https://www.sciencebase.gov//catalog/file/get/59b6cc06e4b08b1644ddf8b3?f=__disk__f7%2F19%2F08%2Ff719084d841c0419e3a7f9a747c156406e32a85b")
```

In contrast, Tidyverse reads in files and saves them as a `tibble`.
The name "tibble" [comes from the proncentation of "tbl_df()", which was "tibble diff"](https://blog.rstudio.com/2016/03/24/tibble-1-0-0/).


```r
library(tidyverse)
```

```
## ── Attaching packages ────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
## ✔ tibble  1.4.2     ✔ dplyr   0.7.6
## ✔ tidyr   0.8.1     ✔ stringr 1.3.1
## ✔ readr   1.1.1     ✔ forcats 0.3.0
```

```
## ── Conflicts ───────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
adults_tib <- read_csv("https://www.sciencebase.gov//catalog/file/get/59b6cc06e4b08b1644ddf8b3?f=__disk__f7%2F19%2F08%2Ff719084d841c0419e3a7f9a747c156406e32a85b")
```

```
## Parsed with column specification:
## cols(
##   Sample = col_character(),
##   Fluor = col_character(),
##   Copies = col_double(),
##   Inhibited = col_character()
## )
```
Notice how the second read in function tells use more about our data than the first. 

### Why can't I find my own data?

When I cannot find my data file, here are the steps I take.

1. Check your working directory. The working directory is where R lives. That is to say, where R reads from and writes to.
2. Make sure the file is really there. 
3. In RStudio, this may be changed under `Session` -> `Set Working Directory`.
4. In the script, use the command `setwd()` to set it and `getwd()` to view it.  
5. Some notes of files paths:
  - Same folder `read.csv("file.csv")` or `read.csv("./file.csv")`
  - Absolute `read.csv("/Path/to/file.csv")`
  - Relative `read.csv("./folder/file.csv")`
    - `./` is current folder
    - `../` is up one folder, `../../` is up 2 folders, etc. 
  
## Data structures

In the previous section, you created two data objects. 
We can explore or "interrogate" objects in R to learn more about them.
Some useful functions include
  - `print()` (usually the default when you type an objects name)
  - `str()`, `class()`, `unclass()` (to learn what R says an object is)
  - `dim()`, `ncol()`, `nrow()` (to see the size of objects)
  - `summary()` (to get a description of each column)
  - `head()`, `tail()` (to look at the top or bottom of an object)

**Exercise:** Test out these on the three example datasets. For example:


```r
print(adults_df)
print(adults_tib)
```

### Other important data types

Besides data.frames and tibbles, R has other useful data (or object) types. 

- Vectors: 
  - Create: in R using concatenate or combine function: e.g., `c(1, 2, 3)` or `c("A", "B", "C")`
  - Types: `numeric()`, `character()`, `integer()`, `factor()`
  - Change types: `as.x()` e.g,. `as.numeric()`
  - Important for plotting and regression 
- `matrix()`:
  - Only one type (e.g., all numeric or all characters)
  - Any size and dimension ranging
  - Used by some R functions and outputs 
- `data.frame()`
  - Table of vectors
  - All same length, must be 2 dimensional
  - Not all same type
  - `tible()` is an _improved_ versions of `data.frame()`
- `list()`
 - Group of objects
 - Can be different lengths
 - Can be different types

### Comparison of base R and Tidyverse 

**Problems:** Base R lacks a consistent syntax and design. This creates problems including: 

- Base R functions are often hard to read;
- Functions often have non-intuitive syntax;
- Outputs can be clunky and difficult to work with; and
- Stringing together outputs can create difficult to read code.


**Solutions:** The Tidyverse packages.

  - Easy to read and understand
  - Language within R
  - Can "pipe" together multiple functions
  
_What is Tidyverse?_

  - _The Tidyverse is an opinionated collection of R packages designed for data science. All packages share an underlying design philosophy, grammar, and data structures._
  - Hadley's opinionated version of what R should be like.  
  
_Alternatives to Tidyverse?_ 

  - Base R: Slower and harder to read
  - data.table: Harder to read although quicker and works with large (100GB+) data.
  - Python with Panadas: Less developed and fewer tools. Not R. 

_Overview of Tidyverse_

  - Core of 8 packages for everything from data manipulation to plotting
  - 10+ extra packages
  - `tibble()` replaces `data.frame()`
  - Includes two packages, `ggplot2` and `lubridate` covered later

## Data manipulaiton

### Filtering 

**Problem:** We need to separate out the two qPCR assay types used with eDNA and remove the controls. 
We want two new data.frames. One with HEX assay and one with a FAM assay. 
These also should have the negative controls removed. 

**Steps:**

1.  We want to filter by the `Fluor` column. First, we can create the FAM assay data.frame. Second, we can create the HEX data.frame.
2.  We want to remove all of the negative controls.


First, we will use base R.  
Second, we will use the Tidyverse. 

### Useful filtering tools 

R contains many tools for filter. 
These are build upon computer logic. 
Examples include: 


```r
## Is a data entry a?
letters == "a"
## Is a data entry NOT a?
letters != "a"
## Is a data entry a or z
letters == "a" | letters == "z"
## Can also use in %in% command
letters %in% c("a", "z")
## But compare to the reverse 
c("a", "z") %in% letters
## for numbers, greather than or equal to as well
1:5 < 2
1:5 <= 2
## There is also an OR function
1:5 <= 2 | 1:5 == 4
```

#### Creating a FAM data.frame

To do this in Base R, we first filter by FAM:

```r
adults_df_FAM <- adults_df[ adults_df$Fluor == "FAM",]
```

Second, we need to remove the negative controls:  

```r
adults_df_FAM_Samples <- adults_df_FAM[ !grepl("Neg-Con", adults_df_FAM$Sample),]
```

Or, we could have done this in one step using an "and" command:

```r
adults_df_FAM_Samples2 <- adults_df[ adults_df$Fluor == "FAM" & !grepl("Neg-Con", adults_df_FAM$Sample),]
```

Conversely, Tidyverse allows us to do the multiple steps in an easy to read syntax.
First, we specify our `tibble`. 
Then we use the pipe command `%>%` to say we want to continue on to another function.
Second, we  use `filter()` twice. 


```r
adults_tib_FAM_Samples <-  adults_tib %>% 
  filter(Fluor == "FAM") %>%
  filter(!grepl("Neg-Con", Sample)) 
```

#### Exercis

- Which syntax seems easiest for your to read?
- Repeat the above exercise extracting `HEX` rather than `FAM`.

***Course note:** For the rest of the course, I will only be using the Tidyverse. 


### More data formatting 

We often want to summarize data. 
The Tidyverse contains many useful tools for doing this. 

#### Basics of Tibbles

The underlying theory behind Tibble is inspired by SQL as well as Hadley's view of [literate programming](https://en.wikipedia.org/wiki/Literate_programming).
Guiding ideas include:

1. Function like `select()` to select columns rather than `df$col`


```
## # A tibble: 352 x 2
##    Fluor  Copies
##    <chr>   <dbl>
##  1 FAM   1336000
##  2 FAM   1099000
##  3 FAM   1229000
##  4 FAM   1827000
##  5 FAM   1758000
##  6 FAM   1543000
##  7 FAM        NA
##  8 FAM        NA
##  9 FAM        NA
## 10 FAM        NA
## # ... with 342 more rows
```

2. `summarize` in Tidyverse



```
## # A tibble: 2 x 2
##   Fluor `mean(Copies, na.rm = TRUE)`
##   <chr>                        <dbl>
## 1 FAM                        470533.
## 2 HEX                        313486.
```

```
## # A tibble: 2 x 3
##   Fluor meanCopies     N
##   <chr>      <dbl> <int>
## 1 FAM      470533.   176
## 2 HEX      313486.   176
```

```
## # A tibble: 6 x 4
## # Groups:   Fluor [?]
##   Fluor `Copies > 100` meanCopies     N
##   <chr> <lgl>               <dbl> <int>
## 1 FAM   FALSE                3.44    17
## 2 FAM   TRUE            545290.     107
## 3 FAM   NA                 NaN       52
## 4 HEX   FALSE                1.50    17
## 5 HEX   TRUE            363292.     107
## 6 HEX   NA                 NaN       52
```

3. Wide versus long data: `gather` and `spread`
  
  - Wide data
  

```r
tib <- tibble(Dose = c("low", "medium", "high"), 
            Rep1 = rbinom(n = 3, size = 6, 0.5),
            Rep2 = rbinom(n = 3, size = 6, 0.5),
            Rep3 = rbinom(n = 3, size = 6, 0.5))
print(tib)
```

```
## # A tibble: 3 x 4
##   Dose    Rep1  Rep2  Rep3
##   <chr>  <int> <int> <int>
## 1 low        4     3     4
## 2 medium     4     3     3
## 3 high       2     5     2
```
  - Long data
  

```r
tibLong <- tib %>%
  gather( Response, value = "Replicate", Rep1, Rep2, Rep3, - Dose)

print(tibLong)
```

```
## # A tibble: 9 x 3
##   Dose   Response Replicate
##   <chr>  <chr>        <int>
## 1 low    Rep1             4
## 2 medium Rep1             4
## 3 high   Rep1             2
## 4 low    Rep2             3
## 5 medium Rep2             3
## 6 high   Rep2             5
## 7 low    Rep3             4
## 8 medium Rep3             3
## 9 high   Rep3             2
```
  - Converting back and forth

```r
tibWide <- tibLong %>% 
  spread(key = "Dose", value = "Replicate")
print(tibWide)
```

```
## # A tibble: 3 x 4
##   Response  high   low medium
##   <chr>    <int> <int>  <int>
## 1 Rep1         2     4      4
## 2 Rep2         5     3      3
## 3 Rep3         2     4      3
```

4. Merging tibbles 
  - `inner_join()`
  - `full_join()`

   

```r
# Create dummy data
a <- tibble(ID = 1:3, A = letters[1:3])
b <- tibble(ID = 1:3, B = LETTERS[1:3])

## Do an inner join
a %>% 
  inner_join(b, by = "ID")
```

```
## # A tibble: 3 x 3
##      ID A     B    
##   <int> <chr> <chr>
## 1     1 a     A    
## 2     2 b     B    
## 3     3 c     C
```

```r
## Try the reverse
b %>% 
  inner_join(a, by = "ID")
```

```
## # A tibble: 3 x 3
##      ID B     A    
##   <int> <chr> <chr>
## 1     1 A     a    
## 2     2 B     b    
## 3     3 C     c
```

```r
## How to use different IDs
b %>% 
  inner_join(a, by = c("ID" = "ID"))
```

```
## # A tibble: 3 x 3
##      ID B     A    
##   <int> <chr> <chr>
## 1     1 A     a    
## 2     2 B     b    
## 3     3 C     c
```


```r
tib1 <- tibble(x=rep(letters[1:2], c(2, 3)), 
               y=1L)
tib2 <- tibble(x2 =rep("b", 3),
               z = 123)

## Compare inner and full joins as well as anti join
tib1 %>%
  inner_join(tib2, by = c("x" = "x2"))

tib1 %>%
  full_join(tib2, by = c("x" = "x2"))

tib1 %>%
  anti_join(tib2, by = c("x" = "x2"))
```
   
   - We can also work with multiple unique keys. Notice keys do not need to have the same names:


```r
first  <- tibble(Day = rep(1:3, 2), Sample = rep(1:2, each = 3), endpoint = 1:6)
second <- tibble(Day = rep(1:3, 2), Observer = rep(1:2, each = 3), cause = 11:16)

third <- first %>%
  inner_join(second, by = c("Day" = "Day", "Sample" = "Observer"))
  
print(third)
```

```
## # A tibble: 6 x 4
##     Day Sample endpoint cause
##   <int>  <int>    <int> <int>
## 1     1      1        1    11
## 2     2      1        2    12
## 3     3      1        3    13
## 4     1      2        4    14
## 5     2      2        5    15
## 6     3      2        6    16
```


## Seeing data with ggplot2

"What is a graphic? How can we succinctly describe a graphic? And how can we create the graphic that we have described?"
-- Hadley Wickham (2010)

**Problem:** Base R's graphics lack a coherent syntax, which limits our ability to explore data with them.

**Solution:** [_Graphics of grammar_](https://www.springer.com/us/book/9780387245447) as implemented in the ggplot2 package.

Base R uses a _pen-and-paper_ philosophy, which means we add things to a plot one command at a time. 
ggplot2 uses its own language to build a plot before plotting.
This makes ggplot2 harder to use until you learns its syntax. 

### Base ggplot2 syntax

`ggplot2` is based upon theory presented in Leland Wilkinson's _Grammar of Graphics_.
This underlying syntax give it power, but makes it hard to learn.
Note that, like in English, it is possible to write syntactically correct, but gibberish text (e.g., "The boat ran to the sky.").
Here is a list of some of the important parts of the syntax:

- **aesthetics** are properties of the graphic and are abbreviated **aes**. These include:
    - `position` (`x` and `y`)
    - `color` (of the border of an object)
    - `fill` (of a solid object such as box)
    - `shape`
    - `size`
    - `alpha` is the transparency of an object and may require the `scales` package
- **geometries** are how the data are plotted and are abbreviated **geom**. These include:
    - `point` plots points
    - `line` plots a line that connects points by order of `x`
    - `path` plots a line that connects points by order of in the `data.frame`
    - `jitter` plots points that are jittered (i.e., not on top of each other)
    - `histogram` plots a histogram of the data
    - `bar` plots a bar graph
    - `boxplot` plots a boxplot of the data
    - `violin` plots a violin plot of the data (similar to a boxplot)
    - `smooth` plots a smoothed line (e.g., gam, loess, lm) to the data
    - `polygon` connects the dots to plot a polygon
    - `ribbon` shades the area between two lines
    - `density` plots a density plot
    - `abline` uses a `slope` and `intercept` to plot a line
- **statistics** may also be plotted are abbreviated **stat** 
- Data may be split by **facet**s
- Subplots may also be **wrap**ped  (similar to faceting, but only one variable)

The implementation of `ggplot2` in `R` requires a base object, `ggplot()` that may be an empty function. 
However, anything added to this does not need to be set elsewhere.
This will make more sense when we start with the code.

### A simple plot: One piece at a time

What does the sea lamprey data look like?
Here, we'll walk through plotting a dataset to examine this question with these steps:

- Load the the sea lamprey dataset
- Replace NAs with 0 
- Remove the controls
- Extract out sample densities 
- Create a simple plot
- Add things to the plot


```r
library(ggplot2)
adults_tib <- read_csv("https://www.sciencebase.gov//catalog/file/get/59b6cc06e4b08b1644ddf8b3?f=__disk__f7%2F19%2F08%2Ff719084d841c0419e3a7f9a747c156406e32a85b")

## Replace missing values and controls
adults_tib_Samples <- adults_tib %>%
  filter(!grepl("Neg-Con|FB|Well|CB", Sample)) %>%
  replace_na(list(Copies = 0))


## Extract out sample density and convert to numeric
adults_tib_Samples <- 
  adults_tib_Samples %>% 
  mutate(Sample2 = as.numeric(gsub("(\\d+)(L-*\\d+[A-Z])", "\\1", Sample)))


## Create simple plot
ggplot(data = adults_tib_Samples, aes(x = Sample2, y = Copies)) + geom_point()

## which could also be created this way
ggplot() + geom_point(data = adults_tib_Samples, aes(x = Sample2, y = Copies))

## But this is hard to see, so let's log10 scale it
ggplot(data = adults_tib_Samples, aes(x = factor(Sample2), y = Copies + 1e-3)) + 
  geom_point() +
  scale_y_log10() 

## And now update the lables 
ggplot(data = adults_tib_Samples, aes(x = factor(Sample2), y = Copies + 1e-3)) + 
  geom_point() +
  scale_y_log10() +
  ylab(expression("log"[10]*"(copy number)")) +
  xlab("Adult lamprey stocking density per tank") +
  theme_bw() 

## Also, what about the two assays? Can we chnage color and shape?
ggplot(data = adults_tib_Samples, aes(x = factor(Sample2), y = Copies + 1e-3, color = Fluor, shape = Fluor)) + 
  geom_point() +
  scale_y_log10() +
  ylab(expression("log"[10]*"(copy number)")) +
  xlab("Adult lamprey stocking density per tank") +
  theme_bw() +
  scale_color_manual("Assay type", values = c("red", "blue"))

## Points overlaps, what about facets?
ggplot(data = adults_tib_Samples, aes(x = factor(Sample2), y = Copies + 1e-3)) + 
  geom_point() +
  scale_y_log10() +
  ylab(expression("log"[10]*"(copy number)")) +
  xlab("Adult lamprey stocking density per tank") +
  theme_bw() +
  facet_grid(. ~ Fluor) +
  theme(strip.background = element_blank())
```

### Subgroupings

Many options are available for breaking out groups with `ggplot2`.
Deciding how to break your dataset into subgroups can be tricky, but is very useful for visualizing data.
Often times, I try something, tinker with it, and try something else until I end up with a plot that makes sense. 
Here is a rough formula of what I would do:


- Decide what is my response variable or variables of interest (e.g., `x`s and `y`s). If I only have 1 continuous variable, decide what is the second most important variable.
- Plot a simple x and y point plot
- Start breaking things down by color, shape, facet, etc.
- Look at marginal plots (e.g., pooling all of the subgroupings for all parameters other than one).


Here is an example from the USFWS, USGS, and U of Minnesota researchers.
The data is from Minnesota and looks at wolf depredations.
Here's how I would start to examine it (as a quantitative person, I'm often handed datasets and asked to explain what is going on without a strong sense of why I'm looking at it): 



```r
library(ggplot2)
library(tidyverse)
library(scales)
library(car) # load package with dataset

ggplot(data = Depredations, aes(x = number)) + 
    geom_histogram()

## Note, we a message about binwidth. This can be important for histograms because it 
## can change how we view the data. Let's see what happens if we change it:
ggplot(data = Depredations, aes(x = number)) + 
    geom_histogram(binwidth = 5)

ggplot(data = Depredations, aes(x = number)) + 
    geom_histogram(binwidth = 10)

ggplot(data = Depredations, aes(x = number)) + 
    geom_histogram(binwidth = 20)

## How do the figures change? 

## Now, we need to "melt" the data so that we may plot it with ggplot    
d2 <- Depredations %>% as.tibble(.) %>%
  gather( number, value = "kills",  late, early)

## Also change number to be time
colnames(d2)[3] <- "TimePeriod"


## Let's talk a stab at plotting this
ggplot(data = d2, aes(x = kills, fill = TimePeriod)) + 
    stat_density() +
    scale_fill_manual(values = alpha(c("blue", "red"), 0.25))

## But notice the data includes a lot of zeros. What if we remove them? 
ggplot(data = d2[ d2$kills > 0,], aes(x = kills, fill = TimePeriod)) + 
    stat_density() +
    scale_fill_manual(values = alpha(c("blue", "red"), 0.25))

## Let's look at a boxplot
ggplot(data = d2, aes(y = kills, x = TimePeriod)) + 
	geom_boxplot()

## With the points "jittered" on top:
ggplot(data = d2, aes(y = kills, x = TimePeriod)) + 
	geom_boxplot() + geom_jitter()

## and now the non-zero events only
ggplot(data = d2[ d2$kills > 0,], aes(y = kills, x = TimePeriod)) + 
	geom_boxplot()

## Let's create a non-zero data frame 
d3 <- d2 %>% 
    filter( kills > 0, )

ggplot(d3, aes(x = longitude, y = latitude, color = kills)) +
    geom_point()

## Now, let;s make spatial plot and examine scaling the data

ggplot(d3, aes(x = longitude, y = latitude, color = kills)) +
    geom_point() +
    scale_color_gradient(low = "skyblue", high = "navyblue", 
                         trans = "sqrt")   

ggplot(d3, aes(x = longitude, y = latitude, color = kills)) +
    geom_point() +
    scale_color_gradient(low = "skyblue", high = "navyblue", 
                         trans = "sqrt") + 
    facet_grid( ~ TimePeriod) 

ggplot(d3, aes(x = longitude, y = latitude)) +
    stat_density2d() + geom_point() +
    facet_grid( ~ TimePeriod) 


ggplot(d3, aes(x = longitude, y = latitude)) +
    stat_density2d(aes(fill = ..level..), geom="polygon") + 
    geom_point() +
    facet_grid( ~ TimePeriod)

## Clean up for publication quality figure
d3$time2 <- d3$time  
levels(d3$time2) <- c("Post-1991", "Pre-1991") 
head(d3)
d3$time2 <- factor(d3$time2, levels = levels(d3$time2)[c(2, 1)])
head(d3)
levels(d3$time2)

finalWolf <- 
    ggplot(d3, aes(x = longitude, y = latitude)) +
    stat_density2d(aes(fill = ..level..), geom="polygon") + 
    geom_point() +
    facet_grid( ~ time2) + 
    theme_bw() +
    ylab(expression("Latitude ("*degree*"N)")) +
    xlab(expression("Longitude ("*degree*"W)")) +
    scale_fill_gradient("Relative\nPredation\nDensity",
                        low = "skyblue", high = "navyblue", 
                         trans = "sqrt") + 
    theme(
          strip.background = element_rect(colour = NA, fill = NA),
          panel.border = element_rect(colour = "black")
          )
print(finalWolf)
```


Note that we may also "save" a plot to an object in `R` and add to it that way as well:


```r
p <- ggplot(data = d, aes(x = Temp, y = Ozone, 
        color = Wind, size = Solar.R)) + geom_point() 
print(p)
print(p + scale_color_gradient(low = "skyblue", high = "navyblue"))
```



### Trends

Often times, we are interested in looking for trends in data.
For example, do chicks increase in weight?
Does this this increase in weight depend upon the feed type?
Or, we may be interested in the relationship between two variables.
Here is an example of how I would explore the classic "ChickWeight" dataset.


```r
data(ChickWeight)
head(ChickWeight)
summary(ChickWeight)

ggplot(data = ChickWeight, 
        aes(x = as.factor(Diet), y = weight)) +
        geom_boxplot()

ggplot(data = ChickWeight, 
        aes(x = Time, y = weight)) +
        geom_point()

ggplot(data = ChickWeight, 
        aes(x = Time, y = weight, group = Chick)) +
        geom_line()

ggplot(data = ChickWeight, 
        aes(x = Time, y = weight, group = Chick, color = Diet)) +
        geom_line()

ggplot(data = ChickWeight, 
        aes(x = Time, y = weight, color = Diet, fill = Diet)) + 
        geom_point()  + stat_smooth()

ggplot(data = ChickWeight, 
        aes(x = Time, y = weight, color = Diet, fill = Diet)) + 
        geom_point()  + stat_smooth(method = "lm")

ggplot(data = ChickWeight, 
        aes(x = Time, y = weight)) + 
        geom_point()  + stat_smooth(method = "lm") +
        facet_grid( . ~ Diet)

summary(lm(weight ~ Time * Diet, data = ChickWeight))
```

### Map example 

R is also becoming an increasingly powerful tool for GIS. 
This example demonstrates a simple map. 


```r
## Load libraries and data
library(tidyverse)
library(car) # load package with dataset
library(maps)

## Load wolf kill data
data(Depredations)

## Load MN outline 
MN_outline <- data.frame(with(maps::map('state', 'Minnesota'), cbind(x,y)))
## Cleanupd data
head(Depredations)

## Now, we need to "melt" the data so that we may plot it with ggplot    
d2 <- Depredations %>% as.tibble(.) %>%
  gather( number, value = "kills",  late, early) %>%
  filter(kills > 0)

## Also change number to be time
colnames(d2)[3] <- "TimePeriod"
 
## record factor levels
level_key = list(late = "Post-1991", early = "Pre-1991")
d2$TimePeriod <- recode(d2$TimePeriod, !!!level_key)

 ## Old plot
finalWolf <-
  ggplot(d2, aes(x = longitude, y = latitude)) +
	stat_density2d(aes(fill = ..level..), geom="polygon") +
	geom_point() +
	facet_grid( ~ TimePeriod) +
	theme_bw() +
ylab(expression("Latitude ("*degree*"N)")) +
xlab(expression("Longitude ("*degree*"W)")) +
scale_fill_gradient("Relative\nPredation\nDensity",
low = "skyblue", high = "navyblue",
trans = "sqrt") +
 theme(
strip.background = element_rect(colour = NA, fill = NA),
panel.border = element_rect(colour = "black")
)
print(finalWolf)

## Make pub quality 

newPlot <- finalWolf + geom_path(data= MN_outline, aes(x =x ,y = y))
  
print(newPlot)
```

### Publication quality figures

- You'll often times need to change a `factor`'s order like we did in the wolf example for either facets or discrete variables.
- The `theme_options()` has useful attributes
- `ggplot2` has themes, the default has a gray background, the `theme_bw` often looks better, but it is personal taste. I also like `theme_minimal`
- `ggthemes` package has some themes
- The `scale` function is helpful, e.g.: `scale_color_discrete` or `scale_fill_continuous` which can also be used with shapes, linetype, etc.
- Use `ggsave` to save your plot.
- If absolutely necessary, touch up your graphic with another program such as Inkscape (if you are a student, I would recommend getting Adobe Illustrator. Adobe Illustrator seems to place nicer with `ggplot2` figures).

### Where to go for more ggplot2 help?

For plotting, I oftentimes browse online to find a plot I like. 
Then I take it, adapt the code, and make it my own.
Last, I save the code for later and repeat.

- `ggplot2` book by Wickham. There is now a second edition out. 
- Google is your friend.
- _R Cookbook_ online: http://www.cookbook-r.com/
- `ggplot2` documentation online 
- `ggplot2` mailing list
- `stackoverflow.com` 

## lubridate

Dates were hard to work with R. 
The lubridate packages makes them much, much easier.


```r
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following object is masked from 'package:base':
## 
##     date
```

```r
test    <- c("10-5-2019", "5-16-2019", "11-7-2012")
testOut <- mdy(test)
str(test)
```

```
##  chr [1:3] "10-5-2019" "5-16-2019" "11-7-2012"
```

```r
str(testOut)
```

```
##  Date[1:3], format: "2019-10-05" "2019-05-16" "2012-11-07"
```

```r
y <- 1:3
lm(y ~ test)
```

```
## 
## Call:
## lm(formula = y ~ test)
## 
## Coefficients:
##   (Intercept)  test11-7-2012  test5-16-2019  
##             1              2              1
```

```r
lm(y ~ testOut)
```

```
## 
## Call:
## lm(formula = y ~ testOut)
## 
## Coefficients:
## (Intercept)      testOut  
##  12.8533219   -0.0006279
```

## Models in R: A crash course of stats in R

A t-test is a special case of ANOVA:


```r
set.seed(123)
a <- rnorm(n = 10, mean = 1, sd = 1)
b <- rnorm(n = 10, mean = 3, sd = 1)
dat <- data.frame(predictor = rep(c("a", "b"), each = 10),
                  response = c(a, b))
t.test(x = a, y = b, var.equal = TRUE)
summary(aov( formula = response ~ predictor,  data = dat))
```

Which is a special case of linear model:


```r
# fit an ANOVA to the data
aovOut <- aov( formula = response ~ predictor,  data = dat)
summary(aovOut)

# fit a linear model to the data
lmOut <- lm( formula = response ~ predictor, data = dat)
summary(lmOut)

# run an ANOVA on the linear model
anova(lmOut)
```

And is a special case of generalized linear models:


```r
# fit a linear model to the data
summary(lm(  formula = response ~ predictor, data = dat))

# fit a generalized linear model to the data
summary(glm( formula = response ~ predictor, data = dat, family = 'gaussian'))
```


Useful functions on models:

- `plot()`
- `print()`
- `summary()`
- `coef()`
- `confint()`
- `predict()`


# Where to from here?

- Dive into R! The more you use it, the better you will become.
- Invest time honing your skills
- Resources 
  - Google
  - Books
    - [R for Data Science](http://r4ds.had.co.nz/)
    - [Modern Dive](http://moderndive.com/)
    - [Spring Book on ggplot2, 2nd edition](https://www.springer.com/us/book/9783319242750)
    - Online tutorials, paid and free
