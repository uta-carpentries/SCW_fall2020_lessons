# Software Carpentry Workshop

## Lesson2: Introduction to R
This lesson is based on [this Software Carpentry lesson](http://swcarpentry.github.io/r-novice-gapminder/)

#### Please make sure your directory structure is setup as described [here](https://github.com/uta-carpentries/SoftwareCarpentryWorkshops_general/blob/master/Data_DirectoryStructure_Setup.md)

Before we start talking about R, let's copy `gapminder.txt` file from `SCW/Data/` to `Lesson2_IntroToR` and take a look at our dataset in Excel. This dataset contains information about life expectancy, population sizes and gdp per capita in different countries for different years. Let's see how we can use R to analyze this dataset. 

  ```bash
    #in Bash/Terminal, do you remember what to do?
    $ cd Desktop/SCW/Data
    
    #to check to see that you are where your file is
    $ ls
    ByCountry/  gapminder.txt

    $ cp gapminder.txt ../Lesson2_IntrotoR/
    
    #to check that it was copied properly
    $ ls ../Lesson2_IntrotoR/
    gapminder.txt
  ```

### Learning objectives
- Understand benefits of using R
- Understand how to work with RStudio
- Get data from Excel to R
- Use the building blocks of R language
- Extract parts of the dataset
- Write simple R scripts

## 1. Intro to R and RStudio

###  Why R?

* Statistics, graphics, general purpose programming
* Thousands of packages available - these are collections of functions that implement all kinds of analyses of data sets from various disciplines
* Open source software - use for free, modify as you wish
* Active community of developers - new packages are being written as we speak

### RStudio as interface for R (IDE - integrated development environment)
We will be working with R using RStudio. This is a piece of software (also known as integrated development environment, IDE ) that makes working in R much easier. When you open RStudio, you should see 4 windows:

* The 4 windows of RStudio:
    * Top left = text editor,write your commands/code here
    * Bottom left = R console, run (execute) your commands here (interactive mode)
    * Top right = things that R keeps track of:
        * History tab records all the commands you type in R console
        * Environment tab keeps track of all objects you create in the current session
        * Both records can be saved for later as .Rhistory and .RData files
    * Bottom right = several helpful tabs, we will see how to use them later. For now, notice that 'Files' tab allows you to navigate between folders.
 
 ![image of Rstudio interface](https://datacarpentry.org/r-intro-geospatial/fig/01-rstudio-script.png "RStudio Interface")
 
 ### Navigating to the `Lesson2_IntrotoR` working directory
 For this workshop we need to navigate to `Lesson2_IntroToR` folder. Many of you will be defaulted in the Documents folder as the current working directory. (You can change your `global options` in the Tools menu.) To change the working directory for the current environment, follow either the GUI steps or the Console steps below.
 
 #### GUI Steps:
 Click three dots icon at the top right corner of the 'Files' tab and navigate to `Desktop/SCW/Lesson2_IntroToR`.  You should see `gapminder.txt` file here. Now click 'More' and select 'Set as working directory'. Notice the change in your console window  - your work with R is now done from `Lesson2_IntroToR` folder.
 
 #### Console Steps:
  ```r
  #One option is to include the path.
  setwd("C:/Users/peace/Desktop/SCW/Lesson2_IntroToR")
  
  #Another option for Windows users is to use choose the folder or file interactively using choose.dir() and file.choose().
  setwd(choose.dir())
  
  #to check where you are use getwd().
  getwd()
  [1] "C:/Users/peace/Desktop/SCW/Lesson2_IntroToR"
  ```
  
  ### Beginning in R Studio
When you type commands in the console window and press 'ENTER', they are executed immediately and the output is displayed. Here are few examples:  
   ```r
   > 3+5
   > sqrt(64) 
   ```
            
   * The `>` symbol means that the R is ready for the next command. If you enter incomplete commands, you will see `+` which means that the system is waiting for you to complete the command. You can always press 'Esc' to return to `>` when stuck with `+` at the prompt.  
   * There is a handy feature that allows you to enter commands without typing them all out (known as autocomplete). For example, instead of typing `sqrt`, if you type `sq` and press `tab`, you see all words that start with `sq`. You can select the command you are looking for and press `enter`.  
   * Notice also that when you type a parenthesis `(` it automatically gives you both the opening and the closing 
brackets `()`. Type 64 inside the parentheses, hit `enter` and the output is your result. R console behaves similarly with quotes.  

   ```r
   > sqrt(64)
   > print("How are you?")
   ```

   Notice that when you select `sqrt` and `print` with autocomplete feature, they come with parentheses, like so: `print()` and `sqrt()`. This is because these commands call functions and functions often need arguments. Function arguments(inputs to the function) are supplied inside the parentheses.

### Writing simple R scripts

   It is often the case that we need to reuse our commands. An R script (or any other script) is a series of commands that are executed in the order they are written. The commands that we have executed one by one in R studio can be written to a text file and then executed all at once by running the file (which is now an R script). R scripts usually have .R extensions. 
  
   To write an R script, you can type commands in the text editor window and save them as a text file. 
Let's open a new R Script file by clicking the `+` icon on the top left corner of scripting panel, choosing R Script, and writing our command there, for example `print("Good morning!")`. To check if this command works, you can send it for execution to console with `CTRL +Enter` click. Once you know you have a command that works, you can save the file and reuse the commands later.  
   We have a very simple example here, but you can imagine writing hundreds of commands in the order you want them to be executed to accomplish a certain task. This is what an R program or R script is. Let's go ahead and begin filling in this script.
   It is a good practice to comment your code. The comments (statements that are helpful to the user, but are not executed) in R start with `#`.  
   Let's add a comment to our simple script.

   ```r
    #my first R command 
    print("Good morning")
   ```
    
   Let's save our script as `R_commands.R` file in `Lesson2_IntroToR` folder. Notice, this file is now visible inside `Lesson2_IntroToR` folder in the bottom-right pannel under `Files` tab.
    

## 2. Building blocks of R

Let's work in scripting mode from now on so that you will have the record of all commands we used in this lesson.

### Variables/objects

One of the main concepts of any programming language is a notion of a **variable**. Variables are created to store values for future use. 
To assign a value to a variable in R, use `<-`assignment operator. The keyboard shortcut is
* For Windows: `Alt+-`
* For Macs: `Option+-`
```r
### Variables

#variable `name` that stores value "Jane"
name <- "Jane"
print(name)

#variable `price` that stores value 3.99
price <- 3.99
print(price)

### working with environment
#remember what env does? it stores the objects you created. Let's see what the environment tab show us.
#How to see the list of variables on the screen?

#list all objects in your environment
ls()

#how to remove an object?
#rm(objectName)
rm(price)

#remove all objects, clear environment
rm(list=ls()) 

```

**A note on variable names:**
* NO SPACES in names
* DO NOT START with numbers or underscores
* R distinguishes between capital letters and lowercase letters
* Names should be MEANINGFUL & CONSISTENT - help yourself and others to understand your code! 


<mark>**Challenge 1:**</mark> Assigning values to variables
    
```
TASK: What will be the value of each variable after each statement is executed in the following code?

mass <- 47.5
age <- 122
mass <- mass * 2.3
age <- age - 20
height <- height + 20
        
```
As you can see, a variable is assigned a value equal to the value of the evaluated expression on the right side of the assignment operator. But what about `height`?

**Challenge 1: Answer**

> ```r
> > mass
> [1] 109.25
> > age
> [1] 102
> > height
> Error: object 'height' not found
> ```

### Functions

In general, a function takes an input and transforms it according to the function's definition(rules). 
You can recognize functions in R by the presence of parantheses. Function's **arguments** are supplied inside parantheses.
```r
###applying square root function
mass<-64                #mass is a variable
sqrt(mass)              #sqrt() is a function with `mass` as its argument
res<-sqrt(mass)         #variable that stores the output of sqrt(mass)function

#In the example above, the square root function takes `mass` object as input
#and finds the square root of its value. The result is then assigned to `res` variable. 

###applying getwd() function
getwd()

#In our second example, `getwd()` is a function that outputs your current location
#within the file system. Although there is no input (many functions do not require arguments), 
#parentheses are still required for a proper syntax in R.
```

There are thousands of built-in functions in R. 
There are also help functions that you can use to find out what function do and how to use them. 
The help appears in the bottom-right window of the RStudio.

```r
### helpfunctions

?plot
help(print)

```

The functionality of R is expanded by R packages that include functions not present in the default installation of R. 
When you need to use another package, do these 2 things:

```r
### working with additional packages 
The functionality of R is expanded by R packages that include functions not present in the default 
installation of R. 
When you need to use another package, do these 2 things:

#install package called "knitr"
install.package("knitr") 

#load package into R
library(knitr)
```

You can also check which packages are installed.

```r
installed.packages()
```

### Data types and Data structures


#### Smallest units in R: single-element data structures

Let's assign value of 45 to a variable `age`. We just created the smallest object in R:
```r
age <- 45

#some useful functions to know more about the object 
length(age)
str(age)
```
Variables can hold values of various types. Most common data types:

* numeric(double+integer)
* character
* logical
* complex
* ...

The most common numeric classes used in R are integer and double (for double precision floating point numbers). R automatically converts between these two classes when needed for mathematical purposes.

To find out the data type of an object, use `typeof()` function:

```r
score <- 79
typeof(score)
is.integer(score)
typeof(is.integer(score))
```
The last expression is an example of a nested function. Nested functions are very common in R, but are very difficult to understand at first. You can always split nested function into a series of single function calls. Remember that the variable inside the most inner parenthesis is an argument(input)for the function that will be evaluated first. In this case, function `is.integer(score)` is evaluated first.

#### Piping in R
**Chaining** means that you invoke multiple method calls. As each method returns an object, you can actually allow the calls to be chained together in a single statement, without needing variables to store the intermediate results.
If you prefer piping to nested functions, you can use packages like **tidyverse** or **magrittr** which use the `%>%` notation as piping, read as "THEN." To type `%>%`, the keyboard sortcut it Ctrl+Shift+M.
The notation goes from `function(argument)` and instead is written as `argument %<% function()`. If there are more than one arguments, you continue to place the others in the brackets. 
```r
install.packages("magrittr")
library(magrittr)

#What would you use instead of sqrt(sum(score, 42))?
score %>% sum(42) %>% sqrt()

#Can you do the same for the original nested function?
score %>% is.integer() %>% typeof()
```

<mark>**Challenge 2:**</mark> Learn how to read the output of nested functions and pipelines
```
TASK: Break the following expression into multiple single function calls. (Optional) Provide the expression as a pipeline.
You will need to assign the output of each function to a variable that
will serve as an input(argument) for the next function. 
What is the value of each variable? What does each function do? 
Assign: `score<-79`

is.logical(is.numeric(typeof(is.integer(score))))
```
**Challenge 2: Answer**

> ```r
> score <- 79
> step1 <- is.integer(score)
> print(step1)
> step2 <- typeof(step1)
> print(step2)
> step3 <- is.numeric(step2)
> print(step3)
> step4 <- is.logical(step3)
> print(step4)
> 
> ## Or as a single step:
>
> # nested functions
> print(is.logical(is.numeric(typeof(is.integer(score)))))
>
> # pipeline
> score %>% is.integer() %>% typeof() %>% is.numeric() %>% is.logical()
> ```

Sometimes you will need to convert between data types. There are functions that do that: `as.integer()`, `as.character()`, and so on. The conversion between data types is not always possible. Let's see what happens here:

```r
score <- 79
typeof(score)
score <- as.integer(score)
typeof(score)
#but can we convert character to integer?
name <- "Sasha"
typeof(name)
name <- as.integer(name)
# the data type will be changed, but no value will be assigned
typeof(name)
print(name)   # NA = missing value
```


#### Data structures with multiple elements
We can combine single elements into collections of items.
Look at the gapminder dataset again. 
Our smallest unit can represent a single element in the dataset, like individual year, or individual country, 
but what would be the simplest object that you can make with multiple elements?

* **Vectors**: collection of elements of the same data type
    * what part of our dataset can be represented by a vector?
    * how to create: use concatenate function, `c()`
    ```r
    ###let's make a vector
    v<-c(1:3, 45)
    v

    #examine the object
   
    length(v) # what does this do?

    str(v)    # tells you the structure of the object - VERY USEFUL useful function

    #view
    head(v, n=2) or head(v, 2) #look at the first 2 elements

    #what would `tail()` do?
    tail(v, n=3)  #look at the last 3 elements

    #manipulate
    v <- c(v,56)  #add element to vector
    
    #vectorizarion 
    v1 <- 2*v   # multiply each vector element by 2
    v1

    # let's try to add vector, let's add v1 and v2, let's create v2
    v2<-c(1:5)
    v3 <- v1+v2
    v3

    #you can also create a character vector:
    v4 <- c("Jane", "John", "Mary")
  
    # change data type
    v3 <- as.character(v3)  #also known as coersion
    str(v3)
    ```
    
* **Matrices**: 2-dimensional vectors that contain elements of the same data type
    * how to create: use `matrix()` function
    ```r
    m <- matrix(c(1:18), 3,6)
    m
    # try functions that we used for vectors - do they work on matrices?
    # new to 2D structures
    dim(m)  # tells you number of rows and columns in your matrix
    ```
    
* **Factors**: special vectors used to represent categorical data
    * what part of our dataset can be represented by a vector?
    * to create: use `factor()`
    ```r
    ## let's look at our dataset gapminder.txt
    ##Let's say continent is a category with different levels (continent names)
    #Let's create a factor continent with the names of the continent in our data
    cont <- factor(c("asia","europe","america","africa", "oceania")) 
    cont
    str(cont)             # what are these numbers in the output?
    typeof(cont)          # integer # factors are of integer data type! Levels are numbered in alphabetical order
   
    ```

* **Lists** : generic vectors - collection of elements with different data types
    * what part of our dataset can be represented by a list?
    * to create: use `list()` function
    ```r
    l<-list("Afghanistan", 1952, 8769855)
    print(l)
    typeof(l)
    str(l)
    length(l)
    ```
    
    Let's clear our environment.
    ```r
    rm(list = ls())
    ```
    
     <mark>**Challenge 3:**</mark> Creating using data structures
    
    ```
    TASK: Try to create a list named 'myorder' that contains the 
    following data structures as list elements:

    -- Element 1 is a character vector called 'menuItems' of length 4 that 
    lists the menu items you ordered from the restaurant: 
    chicken, soup, salad, tea.

    -- Element 2 is a factor called 'menuType' that describes menu items
    as "liquid" or "solid" categories.

    -- Element 3 is a vector called 'menuCost' that records the cost of each menu item:
    4.99, 2.99, 3.29, 1.89.

    *Hint: Define your elements first, then create a list with them.
    You will need c(), factor() and list() functions
    ```
    **Challenge 3: Answer**
    
    > ```r
    > menuItems<-c("chicken", "soup", "salad", "tea")
    > menuType<-factor(c("solid", "liquid", "solid", "liquid"))
    > menuCost<-c(4.99, 2.99, 3.29, 1.89)
    > myorder<-list(menuItems, menuType, menuCost)
    > ```
        
    Now apply the following functions to the list you created. Try to predict the output before you run the command.
    
    ```r
    length(myorder)
    str(myorder)
    print(myorder)
    ```
    
* **Data frames**
    * Let's go back to gapminder dataset. Could you make an informative guess about how this data structure can be represented in R?

    * Yes! It is a list of vectors of equal length, or a data frame. If we make an example of it as `gapm`, we can see the structure.
    
    ```r
    gapm <- list(country <- c("afghan","albania"),continent <- c("asia","america"),year <- c(1952,1953))
    str(gapm)
    ```
    
    Data frames are extremely useful data structures as they represent table-like datasets. 
    Let's look at our myorder list to see if we can make data frame out of it. 
    Is the list we just made suitable for a data frame? Yes, the elements of the list are vectors of equal size.
    
    Previously we used `list()` to combine our elements:

    * `myorder<-list(menuItems, menuType, menuCost)`
    
    Now let's combine with `data.frame()` function. How? Give it a different name, `myorder_df`.

    ```r
    myorder_df<-data.frame(menuItems, menuType, menuCost)
    
    #now view it!
    myorder_df
    #does it look like our gapminder data set?
    #and check with `str()`
    #anything different compared to str(myorder)
    myorder
    myorder_df
    #output? What is happening with data types? 
    
    str(myorder_df)
    dim(myorder_df)
    ```

### General subsetting rules

Now let's talk about how to take your dataset apart. In general, you can access every element of your data set. You must be able to do that to manipulate and analyze your data. There are three general ways to subset the data:

1. **By position index**: Use `[]` operator
```r
v<-c(2:10)
v

# see what happens here
v[2]
v[c(3:6)]
v[-c(3:5)]

# the above works for lists too, notice that [] returns list, use [[]] to return vector
# try subsetting myorder list we created above
myorder[1]
myorder[[1]]

# for 2D structures like matrices and dataframes provide 2 indices [row, column]
myorder_df[1:3, ] #gets first 3 rows
```

2. **By name**: Use `$` operator for lists and data frames ti extract columns as vectors
```r
myorder_df$menuType
```

3. **By logical vector index**: selects elements corresponding to TRUE values of logical vector
* `>`  greater than
* `<` lesser than                   
* `==` equal to
* `>=` greater than or equal to
* `<=` lesser than or equal to

```r
v<-c(1,5,3,4,5)

# select elements that equal to 5
v1<-v[v==5]
v1

# how does the above work? Try:
v==5   # returns logical vector
#v[v==5] selects element of v that have TRUE values in the output of v==5

# Use `myorder_df` dataframe:select rows that satisfy various conditions
# Diplay logical vector to understand the ouput
df1<-myorder_df[myorder_df$menuType=="solid", ]
df1

df2<-myorder_df[myorder_df$menuCost>3, ]
df2
```


## 3. Overview using our gapminder dataset

Let's return to our gapminder dataset.

Before we examine our data, let's read(load) this dataset into R. There are multiple ways to read data into R. For table-like formats, there are 2 popular functions:

* 1. Use `read.table()` function: `myData<-read.table("gapminder.txt", header = TRUE)`.
    * Take a look at the new object `myData`.
    * A bit hard to see? It is too large to be displayed at the console. Different ways to see what your object looks like:
        * Use `head()` function: `head(myData)`.
        * Look at the top right window, environment tab - gives you a brief summary of the object and double-clicking a data frame opens an Excel-like view of the dataset.
        * always check that you read in a complete data set `dim(myData)` to see if you have the correct number of rows and columns.
* 2. Use `read.csv()` function.
This function is for .csv files (where fields are separated by a comma).

Now we know how to read data frames into R. Let's use R to find out more about the data.

<mark>**Challenge 4:**</mark>  Play with gapminder dataset

```
TASK: Answer the following questions about `myData` object
1. What is overall object structure? What function will you use?
2. Can you tell the data type of the elements in each column?
3. Can you extract 3rd and 5th column of the dataset?
4. Can you extract the list of countries in this dataset?
### Hint: use unique(). ###
5. Can you get a part of this dataset that includes information about Sweden?
6. Can you extract all countries for which life expectancy is below 70?
7. Can you make a new column that contains population in units of millions of people?
```
**Challenge 4: Answer**

> ```r
> 1. str()
> 
> 2. typeof() 
> Will return "list" because
> dataframe is a list of vectors; examine the
> output of str() for details about column data types
> 
> 3. myData[ ,c(3,5)]
> You can use head(myData[ , c(3,5)]) to view
> top 6 rows of the output
> 
> 4. unique(myData[,1]) 
> 
> 5. myData[myData$country=="Sweden", ]
> Here, rows are selected based on logical 
> vector TRUE values - can you view this vector?
> 
> 6. myData[myData$lifeExp<70, ] #similar to Q5
> 
> 7. myData$PopM<-myData$pop/10^6  
> This is a simple way to add a column to a dataframe. 
> You can verify that you added a column with head(myData)
> ```

## 4. Saving R scripts

As you recall, an R script (or any other script) is a series of commands that are executed in the order they are written. Be sure to save your updates.
To run your script from R studio (or R):
```r
source("R_commands.R")
```

**Challenge 5:**  Write your own R script
```
Write a script to calculate mean gdpPerCap for African and European countries.

You might need to read help for 'mean' and 'barplot' functions
?mean
?barplot
```
**Challenge 5: Answer**
```r
##This is  MeanGdp.R script

#read data into R
myDataFull<-read.table("gapminder.txt", header = TRUE)

#select information about Africa
Afri<-myDataFull[myDataFull$continent=="Africa",]

#calculate the mean 
Afri.Mean <- mean(Afri$gdpPercap)

#Do the same for Europe
Europe<-myDataFull[myDataFull$continent=="Europe",]
Euro.Mean <- mean(Europe$gdpPercap)

#Store the mean values in a vector
Afri.Euro.Mean <- c(Afri.Mean, Euro.Mean)
Afri.Euro.Mean


#You can also plot MeanGdp
#open png device to write your plot to 
png("Afri.Euro.Mean.png") 

continents.names <- c("Africa","Europe")

barplot(Afri.Euro.Mean, names.arg = continents.names, col = c("#a8ddb5","#43a2ca"), xlab = "Continents", ylab = "Mean GDP per Capita")

dev.off() 
```

***Summary***

This lesson introduced you to main ideas of programming: variables, functions, data structures and scripts. Now you can write your own simple programs in R and begin understanding R code written by others. Our next R lessons will focus on more advanced features of R programming, data visualization and reproducible research.
