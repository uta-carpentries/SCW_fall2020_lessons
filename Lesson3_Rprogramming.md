# Software Carpentry Workshop

## Lesson3 part one: R programming
Adapted from Software Carpentry's [Functions](https://swcarpentry.github.io/r-novice-inflammation/02-func-R/index.html) and [Control Flow](http://swcarpentry.github.io/r-novice-gapminder/07-control-flow/index.html)

#### Please make sure your directory structure is setup as described [here](https://github.com/uta-carpentries/SoftwareCarpentryWorkshops_general/blob/master/Data_DirectoryStructure_Setup.md)

## Introduction
We have covered basic R usage:
- Reading data files
- Creating and manipulating variables
- Data types
- Calling built-in functions

Now we will cover answers to 3 specific questions. They are as follows.

questions:
- "How can I repeat several operations with a single command in R?"
- "How can I make data-dependent choices in R?"
- "How can I repeat operations for different datasets in R?"

### Objectives:
- "Write user-defined functions with `function()`"
- "Write conditional statements with `if()` and `else`."
- "Write and understand `for()` loops."

### Keypoints:
- "Use `function()` to automate specific tasks."
- "Use `if` and `else` to make choices."
- "Use `for` to repeat operations."

## Setup

1. Open RStudio and set Lesson4_ProgrammingR as your working directory.
2. Copy the gapminder dataset from `Data` folder.
3. Clear your history in R enviroment removing all the variables that your created previously.
4. Open a new R script and read the file as `gapminder <- read.table("gapminder.txt", header = TRUE)`
___

## Creating Functions

Functions are a list of operations/commands that automate something complicated or convenient or both. A function usually gets one or more inputs called arguments. Functions often (but not always) return a value. An example of a function would be the `sqrt()` function. The input (the argument) must be a number, and the output (the return value) is the square root of the input number. Executing a function (‘running it’) is called `calling the function`. An example of a function call is:

`b <- sqrt(a)`

Functions provide:
- a name we can remember and invoke it by
- relief from the need to remember the individual operations
- a defined set of inputs and expected outputs
- rich connections to the larger programming environment

Let’s create a new script, call it `functions_lesson.R`, and write some examples of our own. Let’s define a function `fahrenheit_to_celsius` that converts temperatures from Fahrenheit to Kelvin:

**Input**
```r
fahrenheit_to_celsius <- function(temp) {
  celsius <- ((temp - 32) * (5/9))
  return(celsius)
}
```

We define `fahrenheit_to_celsius` by assigning it to the output of `function`. The list of argument names are contained within parentheses. Next, the body of the function–the statements that are executed when it runs–is contained within curly braces (`{}`). The statements in the body are indented by two spaces, which makes the code easier to read but does not affect how the code operates.

When we call the function, the values we pass to it are assigned to those variables so that we can use them inside the function. The last line within the function is what R will evaluate as a returning value. For example, let’s try running our function. Calling our own function is no different from calling any other function:

**Input**
```r
fahrenheit_to_celsius(32)
```

**Output**  

```## [1] 0```  

**Input**  

```fahrenheit_to_celsius(212)```

**Output**  

```## [1] 100 ```

We’ve successfully called the function that we defined, and we have access to the value that we returned.

**Composing Functions**  
Now that we’ve seen how to turn Fahrenheit into Celsius, it’s easy to turn Celsius to Kelvin:

**Input**  

```r
celsius_to_kelvin <- function(temp_C) {
  temp_K <- temp_C + 273.15
  return(temp_K)
}
```
**Input**
```r
# Freezing Point of water
celsius_to_kelvin(0)
```
**Output**
```
## [1] 273.15"
```

What about converting Fahrenheit to Kelvin? We could write out the formula, but we don’t need to. Instead, we can compose the two functions we have already created:

**Input**
```r
fahrenheit_to_kelvin <- function(temp_F) {
  temp_C <- fahrenheit_to_celsius(temp_F)
  temp_K <- celsius_to_kelvin(temp_C)
  return(temp_K)
}
```
**Input**
```r
# Freezing point of water in Kelvin
fahrenheit_to_kelvin(32)
```
**Output**
```
## [1] 273.15
```
This is our first taste of how larger programs are built: we define basic operations, then combine them in ever-large chunks to get the effect we want. Real-life functions will usually be larger than the ones shown here—typically half a dozen to a few dozen lines—but they shouldn’t ever be much longer than that, or the next person who reads it won’t be able to understand what’s going on.

### Challenge 1
Create a function `MeanlifeExp()`, that takes a continent as its argument and returns the mean life expectancy of that continent. For example `MeanlifeExp("Europe")` returns `71.90369`



Example function call and output:
```r
MeanLifeExp("Europe")
```

```
[1] 71.90369
```
**Solution**

**Input**
```r
MeanLifeExp <- function(Continent) {
  Subset_Continent_LifeExp <- gapminder[gapminder$continent == Continent, "lifeExp"]
  lifeExp <- mean(Subset_Continent_LifeExp)
  return(lifeExp)
}
MeanLifeExp("Europe")
```
**Output**
```
[1] 71.90369
```

Let's say we have the following problem:

> In the gapminder dataset, which continents have the mean life expectancy smaller or larger than 50 years?

How would we approach such a problem? What are the steps that are needed? The concepts in the next sections will help us breakdown this problem into smaller bits and eventually solve it. I want to you think about the concept we learn and how that may be applicable to this problem as we move along the lesson.

## if...else statements

Often when we're coding we want to control the flow of our actions. This can be done
by setting actions to occur only if a condition or a set of conditions are met.
Alternatively, we can also set an action to occur a particular number of times.

There are several ways you can control flow in R.
For conditional statements, the most commonly used approaches are the constructs:

```r
# if
if (condition is true) {
  perform action
}

# if ... else
if (condition is true) {
  perform action
} else {  # that is, if the condition is false,
  perform alternative action
}
```
Say, for example, that we want R to print a message if a variable `x` has a particular value:

**Input**
```r
x <- 8

if (x >= 10) {
  print("x is greater than or equal to 10")
}

x
```
**Output**
```
8
```
The print statement does not appear in the console because x is not greater than 10. To print a different message for numbers less than 10, we can add an `else` statement.

**Input**
```r
x <- 8

if (x >= 10) {
  print("x is greater than or equal to 10")
} else {
  print("x is less than 10")
}
```

**Output**
```
[1] x is less than 10
```

You can also test multiple conditions by using `else if`.

**Input**
```r
x <- 8

if (x >= 10) {
  print("x is greater than or equal to 10")
} else if (x > 5) {
  print("x is greater than 5, but less than 10")
} else {
  print("x is less than 5")
}
```
**Output**

```r
[1] x is greater than 5, but less than 10
```

Important: when R evaluates the condition inside `if()` statements, it is looking for a logical element, i.e., `TRUE` or `FALSE`. This can cause some headaches for beginners. 

### Challenge 2
Calculate the mean life Expectancy (using the previous user-defined function) of Asia. If the life expectancy is greater than or equal to 50, `print("Life Expectancy of Asia is greater than or equal to 50")`, if not `print("Life Expectancy of Asia is lower than 50")`

**Solution**


**Input**
```r
Asia_lifeExp <-  MeanLifeExp("Asia")
if(Asia_lifeExp >= 50){
  print("Life Expectancy of Asia is greater than or equal to 50")
} else {
  print("Life Expectancy of Asia is lower than 50")
}
```

**Output**
```r
[1] "Life Expectancy of Asia is greater than or equal to 50"
```
> Do you think we can apply `if` and `else` to our problem?

## Repeating operations

If you want to iterate over a set of values, when the order of iteration is important, and perform the same operation on each, a `for()` loop will do the job. We saw `for()` loops in the shell lessons earlier. This is the most flexible of looping operations, but therefore also the hardest to use correctly. Avoid using `for()` loops unless the order of iteration is important: i.e. the calculation at each iteration depends on the results of previous iterations.

The basic structure of a `for()` loop is:

```r
for(iterator in set of values){
  do a thing
}
```

**Input**
```r
for(i in 1:10){
  print(i)
}
```
**Output**
```r
[1] 1
[1] 2
[1] 3
[1] 4
[1] 5
[1] 6
[1] 7
[1] 8
[1] 9
[1] 10
```
The 1:10 bit creates a vector on the fly; you can iterate over any other vector as well.

For example, in our previous R lesson we had a `myorder_df`. We could iterate over each `menuItem` and display its cost.

**Input**
```r
menuItems<-c("chicken", "soup", "salad", "tea")  
menuType<-factor(c("solid", "liquid", "solid", "liquid"))  
menuCost<-c(4.99, 2.99, 3.29, 1.89)  
myorder_df<-data.frame(menuItems, menuType, menuCost)

for (items in myorder_df$menuItems){
  myorder_df_subset <-  myorder_df[myorder_df$menuItems == items,]
  print(items)
  print(myorder_df_subset$menuCost)
}
```

**Output**
```r
[1] "chicken"
[1] 4.99
[1] "soup"
[1] 2.99
[1] "salad"
[1] 3.29
[1] "tea"
[1] 1.89
```

> Now, you are equipped with all things necessary to solve our problem.

### Challenge 3

Write a script that loops through the `gapminder` data by continent and prints out whether the mean life expectancy is smaller or larger than 50 years.

*Hint: Try unique() function to get unique values of a column*

**Solution**

```r
gapminder <- read.table("gapminder.txt", header = TRUE)

thresholdValue <- 50

continent_list <- unique(gapminder$continent)

for(continent in continent_list){

  continent_subset <- gapminder[gapminder$continent == continent, "lifeExp"]
  tmp <- mean(continent_subset)
  if(tmp <= thresholdValue){
    print(paste0("Average Life Expectancy in ", continent, " is less than ", thresholdValue))
  }
  else{
    print(paste0("Average Life Expectancy in ", continent, " is greater than ", thresholdValue))
  } # end if else condition
  rm(tmp)
}
```


## Key Points
- Define a function using `function()`.
- The body of a function should be indented.
- Call a function using `name_of_the_function()`.
- Return the result using the `return` statement.
- Use `if` and `else` to make choices.
- Use `for` to repeat operations.


## Lesson3 part 2: Data visualization with ggplot2
This lesson is based on [this Software Carpentry lesson](http://swcarpentry.github.io/r-novice-gapminder/08-plot-ggplot2/index.html)

#### Please make sure your directory structure is setup as described [here](https://github.com/uta-carpentries/SoftwareCarpentryWorkshops_general/blob/master/Data_DirectoryStructure_Setup.md)


## Introduction
R is one of the most powerful programming language for visualizing data. It isoften used to generate publication-quality graphics. Today, we will give you a flavor of some of the quality plotting you can produce using the `R` package [`ggplot2`](http://ggplot2.tidyverse.org/). `ggplot2` is perhaps the best package for intuitive generation of high-quality figures. We will continue using the **gapminder** dataset and will visualize some of the trends in these data with `ggplot2`. Check out some of the interesting dynamic plots available from the [Gapminder website](https://www.gapminder.org/tools/#$chart-type=bubbles). By the end of this lesson you will know the basic principles necessary to produce similar, static versions of many of the example plots you are looking at. 


## Objectives
- To be able to use `ggplot2` to generate publication-quality graphics.
- To understand the basic *grammar of graphics*, including the aesthetics and geometry layers, adding statistics, transforming scales, and coloring or panelling by groups.
#### Keypoints
- Use `ggplot2` to create plots.
- Think about graphics in layers: aesthetics, geometry, statistics, scale transformation, and grouping.


## Background

Plotting our data is one of the best ways to quickly explore it and the various relationships between variables.

There are three main plotting systems in R, the [base plotting system][base], the [lattice][lattice] package, and the [ggplot2][ggplot2] package.

[base]: https://www.rdocumentation.org/packages/graphics/versions/3.6.1
[lattice]: http://www.statmethods.net/advgraphs/trellis.html
[ggplot2]: http://docs.ggplot2.org/current/

Today we'll be learning about the `ggplot2` package, because it is the most effective for creating publication-quality graphics.

`ggplot2` is built on the *grammar of graphics*, the idea that any plot can be generated from the same set of components: a **data** set, a **coordinate system**, and a set of **geoms** (the visual representation of data points).

The key to understanding `ggplot2` is thinking about a figure in layers. This idea may be familiar to you if you have used image editing programs like Photoshop, Illustrator, or Inkscape.
[Main components of ggplot](https://darencard.github.io/public_resources/R/ggplot_intro_slides.pdf)


## Quickstart

We will be working in `Lesson5_DataVisualizationR` folder. Please copy `gapminder.txt` from `Data` folder to `Lesson5_DataVisualizationR` folder. Navigate to `Lesson5_DataVisualizationR` folder in RStudio and set this folder as your working directory.  

We will need to install `ggplot2` package. Let's use console window to do that:
```{r}
install.packages("ggplot2")
```
Now let's work in scripting mode (text editor) so we can save all our commands to file. Open a new file, save as `ggplot.R`. Make sure your new file is visible in `Lesson5_DataVisualizationR`folder under `Files` tab in the bottom-right pannel.

Remember that in order to work with `ggplot2` package, we need to load it into R.
```{r}
#load package into R
library(ggplot2)
```

Now let's load our **gapminder** dataset into `R`.

```{r load_gaminder, message=FALSE}
gapminder <- read.table("gapminder.txt", header=TRUE, sep="\t")

#view the dataset to know what variables are present (or what can be potentially plotted)
head(gapminder)
#or view as a table using environment tab in the top-right panel
```

We are now ready to plot. Let's start off with an example:

```{r lifeExp-vs-gdpPercap-scatter, message=FALSE}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point()
```

So the first thing we do is call the `ggplot` function. This function lets R know that we're creating a new plot, and any of the arguments we give the `ggplot` function are the **global** options for the plot: **they apply to all layers on the plot**.

We've passed in two arguments to `ggplot`. First, we tell `ggplot` what data we want to show on our figure, in this example the gapminder data we read in earlier. For the second argument we passed in the `aes` function, which tells `ggplot` how variables in the **data** map to *aesthetic* properties of the figure, in this case the **x** and **y** locations. Here we told `ggplot` we want to plot the `gdpPercap` column of the gapminder data frame on the x-axis, and the `lifeExp` column on the y-axis. Notice that we didn't need to explicitly pass these columns to `aes` function (e.g. `x = gapminder[, "gdpPercap"]`), this is because `ggplot` is smart enough to know to look in the **data** for that column!

Let's break this long command into parts:
By itself, the call to `ggplot` isn't enough to draw a figure:

```{r}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp))
```

We need to tell `ggplot` how we want to visually represent the data, which we do by adding a new **geom** layer. In our example, we used `geom_point`, which tells `ggplot` we want to visually represent the relationship between **x** and **y** as a scatterplot of points:

```{r lifeExp-vs-gdpPercap-scatter2}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point()
```

And here you have it - your first plot with `ggplot2`!  
The **three components that must be specified** (minimum) to build a plot with `ggplot2` are:

* data
* aesthetic mappings (aes)
* geometric oblects (geom)


> ### Challenge 1
>
> Modify the example so that the figure shows how life expectancy has changed over time:
> 
> ```{r, eval=FALSE}
> ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) + geom_point()
> ```
> 
> Hint: the gapminder dataset has a column called "year", which should appear on the x-axis.
> 
> > #### Solution
> >
> > Here is one possible solution:
> >
> > ```{r ch1-sol}
> > ggplot(data = gapminder, aes(x = year, y = lifeExp)) + geom_point()
> > ```
>
> ### Challenge 2
>
> In the previous examples and challenge we've used the `aes` function to tell the scatterplot **geom** about the **x** and **y** locations of each point. Another *aesthetic* property we can modify is the point *color*. Modify the code from the previous challenge to **color** the points by the "continent" column. What trends do you see in the data? Are they what you expected?
>
> > #### Solution
> >
> > In the previous examples and challenge we've used the `aes` function to tell the scatterplot **geom** about the **x** and **y** locations of each point. Another *aesthetic* property we can modify is the point *color*. Modify the code from the previous challenge to **color** the points by the "continent" column. What trends do you see in the data? Are they what you expected?
> >
> > ```{r ch2-sol}
> > ggplot(data = gapminder, aes(x = year, y = lifeExp, color=continent)) +
> >   geom_point()
> > ```


## Layers

Now let's talk about layers. In `ggplot2`, layers are added with `+` operator, giving an intuitive understanding about the content of each layer. In the above example, `geom_point()` layer contained points.
Now, using a scatterplot probably isn't the best for visualizing change over time. Instead, let's tell `ggplot` to visualize the data as a line plot:

```{r lifeExp-line}
ggplot(data = gapminder, aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line()
```

Instead of adding a `geom_point` layer, we've added a `geom_line` layer. We've added the **by** *aesthetic*, which tells `ggplot` to draw a line for each country.

But what if we want to visualize both lines and points on the plot? We can simply add another layer to the plot:

```{r lifeExp-line-point}
ggplot(data = gapminder, aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line() + geom_point()
```

It's important to note that each layer is drawn on top of the previous layer. In this example, the points have been drawn *on top of* the lines. Here's a demonstration:

```{r lifeExp-layer-example-1}
ggplot(data = gapminder, aes(x=year, y=lifeExp, by=country)) +
  geom_line(aes(color=continent)) + geom_point()
```

In this example, the *aesthetic* mapping of **color** has been moved from the global plot options in `ggplot` to the `geom_line` layer so it no longer applies to the points. Now we can clearly see that the points are drawn on top of the lines.

Here is a full [documentation for ggplot2 package](https://cran.r-project.org/web/packages/ggplot2/ggplot2.pdf). And also [here](https://ggplot2.tidyverse.org/reference/#section-layer-geoms).  What is important here is to know that you can specify these settings for every layer separately as we have seen in the previous example when we specified mapping for geom_line():  `geom_line(aes(color=continent))`.  
  
 

> ### Tip: Setting an aesthetic to a value instead of a mapping
>
> So far, we've seen how to use an aesthetic (such as **color**) as a *mapping* to a variable in the data. For example, when we use `geom_line(aes(color=continent))`, ggplot will give a different color to each continent. But what if we want to change the colour of all lines to blue? You may think that `geom_line(aes(color="blue"))` should work, but it doesn't. Since we don't want to create a mapping to a specific variable, we simply move the color specification outside of the `aes()` function, like this: `geom_line(color="blue")`.

```{r lifeExp-layer-example-1}
ggplot(data = gapminder, aes(x=year, y=lifeExp, by=country)) +
     geom_line(color="blue") + geom_point()
```
> ### Challenge 3
>
> Switch the order of the point and line layers from the previous example. What happened?
>
> > #### Solution
> >
> > Switch the order of the point and line layers from the previous example. What happened?
> >
> > ```{r ch3-sol}
> > ggplot(data = gapminder, aes(x=year, y=lifeExp, by=country)) +
> >  geom_point() + geom_line(aes(color=continent))
> > ```
> >
> > The lines now get drawn over the points!

## Transformations and statistics

`ggplot` also makes it easy to overlay statistical models over the data. To demonstrate we'll go back to our first example:

```{r lifeExp-vs-gdpPercap-scatter3, message=FALSE}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp, color=continent)) +
  geom_point()
```

Currently it's hard to see the relationship between the points due to some strong outliers in GDP per capita. We can change the scale of units on the x axis using the *scale* functions. These control the mapping between the data values and visual values of an aesthetic. We can also modify the transparency of the points, using the *alpha* function, which is especially helpful when you have a large amount of data which is very clustered.

```{r axis-scale}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.5) + scale_x_log10()
```

The `log10` function applied a transformation to the values of the gdpPercap column before rendering them on the plot, so that each multiple of 10 now only corresponds to an increase in 1 on the transformed scale, e.g. a GDP per capita of 1,000 is now 3 on the x axis, a value of 10,000 corresponds to 4 on the x axis and so on. This makes it easier to visualize the spread of data on the x-axis.

> ### Tip Reminder: Setting an aesthetic to a value instead of a mapping
>
> Notice that we used `geom_point(alpha = 0.5)`. As the previous tip mentioned, using a setting outside of the `aes()` function will cause this value to be used for all points, which is what we want in this case. But just like any other aesthetic setting, *alpha* can also be mapped to a variable in the data. For example, we can give a different transparency to each continent with `geom_point(aes(alpha = continent))`.

We can fit a simple relationship to the data by adding another layer, `geom_smooth`:

```{r lm-fit}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point() + scale_x_log10() + geom_smooth(method="lm")
```

We can make the line thicker by *setting* the **size** aesthetic in the `geom_smooth` layer:

```{r lm-fit2}
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point() + scale_x_log10() + geom_smooth(method="lm", size=1.5)
```

> ### Challenge 4
> Part 1.
>
> Modify the color and size of the points on the point layer in the previous example.
>
> Hint: do not use the `aes` function.
>
> > #### Solution to Part 1.
> >
> > Modify the color and size of the points on the point layer in the previous example.
> >
> > Hint: do not use the `aes` function.
> >
> > ```{r ch4a-sol}
> > ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp)) +
> >  geom_point(size=3, color="orange") + scale_x_log10() +
> >  geom_smooth(method="lm", size=1.5)
> > ```

> ### Challenge 5
> Part 2.
>
> Modify your solution to Part 1 so that the points are now a different shape and are colored by continent with new 
> trendlines.  
> Hint: Use color argument inside aes().
>       See [here about shapes](https://ggplot2.tidyverse.org/articles/ggplot2-specs.html#point)
>
> > #### Solution to Part 2.
> >
> > Modify your solution to Part 1 so that the points are now a different shape and are colored by continent with new 
> > trendlines.
> >
> > Hint: Use color argument inside aes().
> >       See [here about shapes](https://ggplot2.tidyverse.org/articles/ggplot2-specs.html#point)
> >
> >```{r ch4b-sol}
> > ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp, color = continent)) +
> > geom_point(size=3, shape=17) + scale_x_log10() +
> > geom_smooth(method="lm", size=1.5)
> > ```

## Multi-panel figures

Earlier we visualized the change in life expectancy over time across all countries in one plot. Alternatively, we can split this out over multiple panels by adding a layer of **facet** panels. Focusing only on those countries with names that start with the letter "A" or "Z".

> ### Tip
>
> We start by subsetting the data. We use `startsWith` function to select names of countries that start with either letter 'A' or 'Z'. This function returns a logical vector. We can then use it to subset rows in `gapminder` dataset.  

```{r facet}
az_rows=startsWith(as.vector(gapminder$country), c('A','Z') )
az_countries <- gapminder[az_rows, ]
ggplot(data = az_countries, aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country)
```

The `facet_wrap` layer took a "formula" as its argument, denoted by the tilde (~). This tells R to draw a panel for each unique value in the country column of the gapminder dataset.

## Modifying text

To clean this figure up for a publication we need to change some of the text elements. The x-axis is too cluttered, and the y axis should read "Life expectancy", rather than the column name in the data frame.

We can do this by adding a couple of different layers. The **theme** layer controls the axis text, and overall text size. Labels for the axes, plot  title and any legend can be set using the `labs` function. Legend titles are set using the same names we used in the `aes` specification. Thus below the color legend title is set using `color = "Continent"`, while the title  of a fill legend would be set using `fill = "MyTitle"`.  `Fill` is used instead of `color` when geoms are filled with color, like bar plots, for example.

```{r theme}
ggplot(data = az_countries, aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x=element_text(angle=45), axis.ticks.x=element_blank())
```

## Exporting the plot

The `ggsave()` function allows you to export a plot created with `ggplot`. You can specify the dimension and resolution of your plot by adjusting the appropriate arguments (`width`, `height` and `dpi`) to create high quality graphics for publication. In order to save the plot from above, we first assign it to a variable `lifeExp_plot`, then tell `ggsave` to save that plot in `png` format.

```{r theme}
lifeExp_plot <- ggplot(data = az_countries, aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x=element_text(angle=45), axis.ticks.x=element_blank())

ggsave(filename = "lifeExp.png", plot = lifeExp_plot, width = 12, height = 10, dpi = 300, units = "cm")
```
**Note** `ggsave` saves the last plot by default, so `plot` argument can be omitted. But if you created plots earlier in your script and want to save them later, you can specify which plot to save.
```
#saves the last plot by default
ggsave("myPlot.pdf")

#can specify what plot to save
ggsave("myPlot.pdf", plot=fp1)
```

This is a taste of what you can do with `ggplot2`. RStudio provides a really useful [cheat sheet][cheat] of the different layers available, and more extensive documentation is available on the [ggplot2 website][ggplot-doc]. Finally, if you have no idea how to change something, a quick Google search will usually send you to a relevant question and answer on Stack Overflow with reusable code to modify!

[cheat]: http://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf
[ggplot-doc]: http://docs.ggplot2.org/current/

Now let's finish this lesson practicing making bar plots!
> ### Challenge 6
> #### Part 1.
>
> Plot life expectancy over years for a country of your choice using geom_bar()
> **Hint** See help for geom_bar: `?geom_bar`
> Understand the difference between `stat="count"` and `stat="identity"`
>
> #### Part 2.
> Prepare a figure for publication(add labels, titles, etc.,) to show population size
> over years for every country that starts with letter 'E'. 
> **Hint** 
> Follow life Expectancy over years example we discussed earlier. Use facet_wrap function.
> 
> #### Part 3.
> Can you explain what information is plotted with this code?
>```{r}
> ggplot(data=gapminder, aes(x=continent, y=lifeExp)) + 
>        geom_bar(aes(fill = continent), stat="summary",fun.y="mean")
>```
>
> > #### Solution to Part 1
> > 
> >```{r}
> > # you must specify stat="identity" to get lifeExp on y axis:
> > ggplot(data =gapminder[gapminder$country=="Sweden", ], aes(x = year, y = lifeExp)) +
> >        geom_bar(fill='orange', stat="identity")
> > 
> > # the default stat for geom_bar() is stat="count". In this case, the number of observations
> > # for every year is plotted:
> > ggplot(data =gapminder[gapminder$country=="Sweden", ], aes(x = year)) +
> >        geom_bar(fill='orange')
> >```
> > #### Solution to Part 2
> > 
> > ```{r }
> > e_rows=startsWith(as.vector(gapminder$country), c('E') )
> > e_countries <- gapminder[e_rows, ]
> > ggplot(data = e_countries, aes(x = year, y = pop/1000000, fill=continent)) +
> >        geom_bar(stat="identity") + facet_wrap( ~ country) +
> >        labs(
> >        x = "Year",                     # x axis title
> >        y = "Population (Million)",     # y axis title
> >        title = "Figure 1",             # main title of figure
> >        fill = "Continent"              # title of legend
> >        ) +
> >        theme(axis.text.x=element_text(angle=45), axis.ticks.x=element_blank()) +
> >        theme_bw()
> > ```
> > 
> > #### Solution to Part 3
> > 
> > A barplot of average life expectancy across years and countries for every continent.
> >


## Demo some more advanced features
If time permits, the following interactive activities can be run to showcase some of the cool stuff you can do with `ggplot` and `R`.

Let's do this in terms of one of the cooler visualizations directly from the [**Gapminder** website](https://www.gapminder.org/tools/#_chart-type=bubbles). This visualization shows the relationship between income and life expectancy for all nations in the dataset. The points are scaled in size based on the population size of the nation and colored based on continent. So there is a lot of details here. 

> ### Challenge 7
>
> Can we create something pretty similar using `ggplot`? What variables in our dataset needs to be mapped to what aesthetics to achive this?
>
> > #### Solution
> >
> > x = income
> > y = life expectancy
> > size = population size
> > color = continent
> >
> ### Challenge 
> 
> Use mappings above to produce a similar plot for 2007. Bonus points if you can use `dplyr` to do it.
>
> >  #### Solution 
> >
> > ```{r ch6b-bubble-plot}
> > # note that you can save plot to variable and plot later
> > library(dplyr)
> > bubble <- gapminder %>%
> >    filter(year == 2007) %>%
> >    ggplot(aes(x = gdpPercap,
> >               y = lifeExp,
> >               color = continent,
> >               size = pop)) +
> >      geom_point() + 
> >      labs(
> >        x = "Income",            # x axis title
> >        y = "Life expectancy"    # y axis title
> >      )
> > bubble
> > ```

This is great, but you'll notice that it this plot is static, while the online one is interactive. Turns out is is actually pretty easy to create an interactive version when you know a little `ggplot`, using a package called `plotly`. Let's demo this.

```{r plotly_demo}
install.packages("plotly")
library(plotly)

# plotly has built in support for `ggplot` objects
bubble <- gapminder %>%
    filter(year == 2007) %>%
    ggplot(aes(x = gdpPercap,
               y = lifeExp,
               color = continent,
               size = pop,
               text = country)) +
    geom_point() + 
    labs(
        x = "Income",            # x axis title
        y = "Life expectancy"    # y axis title
    )
    
ggplotly(bubble)
```

Now you'll see an interactive plot, which is really awesome for exploring and for showing off your data.

Very cool. See how easy it is to produce fancy plots in`R`!
