# R-Notes
--- 
This document is the first of my `R`{.bash}-markdown files. This document contains code
and $\LaTeX$. To use the $\LaTeX$ syntax, use the following in `R`{.bash}-markdown.
```r
output:
  html_document:
    mathjax: local
    self_contained: false
```
## Arithmetic in R
Arithmetic in `R`{.bash} is quite simple. You can run it in the Console or run it line by line in the source file.
R supports $+,-,/,\cdot,$ and even modular arithmetic. Below are some examples.
```r
1+2 #Addition.
5-2 #Subtraction.
5*2 #Multiplication.
5/2 #Division.
5 %% 2 #Modular Arthimetic.
(5*2) + (5-3) #Order of operations.
```
## Variables
When it comes to variables in R there is a different assignment operator. This is the arrow operator `<-`{.r}
Below is how to use this operator on assigning `var`{.bash} the value `5`{.bash}.
```r
var <- 5 #5 is now stored as the variable "var."
```
The naming convention in R is variables are either camel case, or the space between words is represented as a `.`{.bash}
```r
bank.account <- 20 #"period" notation.
bankAccount <-872 #camel case.
```
## Basic Data Types
In R we have a variety of data types like `numberic, logical, character`{.bash}, etc. We can find out what variables data type is by calling a function called `class()`{.r}
```r
var <- 100
trueVar <- TRUE
falseVar <- FALSE
myName <- "Michael Dick"
class(var) #outputs: numeric
class(trueVar) #outputs: logical
class(falseVar) #outputs: logical
class(myName) #outputs: character
```
## Vector Basics
Vectors in R are 1-D arrays. The unique thing about these vectors is that they can act as a dictionary in Python. To initialize a vector in R we use the syntax: `vec <- c(10, 20 ,30)`{.r} where `c`{.bash} is a a function that combines all of these variables to be a part of this array. Now we can associate meaning to certain variable types. Look at the following:
```r
days <- c("Mon", "Tues", "Weds", "Thurs", "Fri", "Sat", "Sun") #Array of characters.
temps <- c(72, 55, 79, 60, 80, 70, 69) #Array of numerics.
names(temps) <- days #names assigns each item in temps a name from days
temps
```
`temps`{.bash} will display the following:
```r
 Mon  Tues  Weds Thurs   Fri   Sat   Sun 
   72    55    79    60    80    70    69 
```

## Vector Indexing and Slicing
With R it is VERY IMPORTANT to remember that indexing in R starts at `1`{.bash} rather than `0`{.bash}. There is a few unique things we can perform on vectors. Let's look at sample code:
```r
v1 <- c(100,200,300)
v2 <- c(a,b,c) 
v1[1] #Returns 100
temps[5] #Returns  Fri 
#                   80 
temps[2:4] #Splicing
#Returns: Tues  Weds Thurs 
#           55    79    60 
temps[c(1,7)] #Grab index 1 and index 7
temps["Mon"] #Returns the number assoicated with "Mon"
temps[c("Tues", "Fri")]
#Filter out values less than 2
vnum <- c(1,2,3,4)
vchar <- c('a', 'b', 'c', 'd')
names(vnum) <- vchar
vnum[vnum > 2] #Returns 3 and 4
vnum > 2
###################################
myFilter <- vnum > 2
vnum[myFilter]
###################################
```
For the `#`{.R} section of this code block you see we assign an array of logical operations. We can call this `myFiler`{.bash}. `myFilter`{.bash} will contain `{FALSE, FALSE, TRUE, TRUE}`{.R} and when we run `vnum[myFiler]`{.R} and this will return all the numbers that are greater than 2. It produces the result: 
```.code
c d 
3 4 
```
## Getting Help in R
To get help in R with variable names, functions, etc., you can easily do this in two ways.
<br>
<br>
1. Using `help()`{.R}, in the parentheses you would add what you need help one. For example, if you wanted help with vectors you would type `help("vector")`{.R} in the Console tab in RStudio.
<br>
<br>
2. Getting help by typing `?`{.bash} in front of what you want help with. Like in the last example, this is what you would use if you want to find more information on vectors `?.vectors`{.bash}

## Matrices in R

When building matrices we will use the built-in function `matrix()`{.bash}

### Syntax for `matrix()`{.bash}
```r
matrix(data = NA, nrow = 1, ncol = 1, byrow = FALSE, dimnames = NULL)
```
`data`{.bash} is what we are going to store in the matrix. By default it will store each entry as a row item. We can specify the number of rows by using `nrow`{.bash} when typing the matrix function. We can specify the number of columns we want by using `ncol`{.bash} when filling in the parameters of `matrix()`{.bash}. `byrom`{.bash} is a parameter in `matrix`{.bash} that is false by default, and this organizes the data fed into the matrix by row rather than column.

### Naming the Rows and the Columns

Let's work by example. We want to create a calendar with the days we are "On," and the days we are "Off."

```r
week1 <- c("On", "On", "Off", "On", "On")
week2 <- c("Off", "Off", "Off", "On", "On")
week3 <- c("On", "On", "On", "On", "On")
week4 <- c("Off", "Off", "On", "Off", "Off")
#Creating a 1D array of variables#
month <- c(week1, week2, week3, week4)
#Naming the matrix workMonth from the 1D array "month"#
workMonth <- matrix(month, ncol = 5, nrow = 4, byrow = TRUE)
#Naming columns from the days array.#
colnames(workMonth) <- days
workweek <- c('1','2','3','4')
#Naming the rows from the workweek vector.#
rownames(workMonth) <- workweek
workMonth
```
## Adding Rows and Columns to a Matrix

There is two new ideas here: `cbind`{.bash} and `rbind`{.bash}. For the syntax for each of these: `rbind(matrixName, rowName)`{.r}

```r
#Exam scores#
eecs183 <- c(93,100,39,55,29,42)
eecs203 <- c(100,23,37,56,98,78)
eecs280 <- c(100,23,94,25,82,45)
eecs281 <- c(81,54,73,65,55,47)
#Putting the class name into a vector#
grades <- c (eecs183, eecs203, eecs280, eecs281)
#Making a matrix to display grades as a table or 2D array#
gradesMatrix <- matrix(grades, nrow = 4, byrow = TRUE)
#Naming rows-start#
classes <- c("EECS183","EECS203","EECS280","EECS281")
rownames(gradesMatrix) <- classes
#Naming rows-end#
#Naming cols-start#
examNum <- c(1,2,3,4,5,6)
colnames(gradesMatrix) <- examNum
#Naming cols-end#

#Displays the sum for EACH column#
colSums(gradesMatrix)
rowSums(gradesMatrix)
rowMeans(gradesMatrix)

#Adding columns and rows to a matrix#
eecs370 <- c(78,88,21,55,91)
#Matrix name is to the right and name of row is the left.#
updatedGrades <- rbind(gradesMatrix, eecs370)
#Adding a column named average#
average <- rowMeans(updatedGrades)
updatedGrades <- cbind(updatedGrades, average)
updatedGrades

```
## Factor and Categorical Matrices
Using R you can give a vector a certain order. When it comes to the idea of, say, that hot is better than cold, how can we show this? Using a function called `factor`{.bash} we can assign this kind of order. Let's look at this example:
```r
animal <- c("dog", "cat", "dog", "cat", "cat")
#ID Number for dog and cat.#
idNum <- c(1,2,3,4,5)
factor(animal)
#Levels cat and dog are now assigned to animal vector.#
factorAnimal <- factor(animal)
#Nominal means there is no order. Ordinal means there is an order.

#Here is an order: cold < med < hot.
temps <- c("cold", "med", "hot", "hot", "hot", "cold", "med")
#We give factor the vector list, tell that this is ordered#
#, and now give the factor function the order that we want.#
factTemps <- factor(temps, ordered = TRUE, levels = c("cold", "med", "hot"))
factTemps
#Prints the number of times each word is present in the vector.#
summary(factTemps)
```
## Data Frames

A big difference between matrix and data frames is that data frames can be of different data types. Also, the rows and columns of a data frame can be labeled. Think of data frames as an Excel spreadsheet. Below are some data frames that are built into R-Studio.
```r
state.x77
USPersonalExpenditure
women
#To see all the datasets in R#
data()
```
Some of these data frames can be quite large. We can look at the first seven entries using `head(nameOfDataSet)`, or the last seven entries using `tail(nameOfDataSet)`.

Now, let's build some of our own data frames. We will first start out by creating some vectors. We have to make sure that all the vectors have the same length. 
```r
#Making vectors.
days <- c("Mon", "Tues", "Weds", "Thurs", "Fri")
temp <- c(78,72,60,55,77)
#T means didn't rain, F means rain.
rain <- c(T,T,T,F,F)
```
Let's put these vectors in a data frame:
```r
data.frame(days, temp, rain)
#Saving this data frame into a variable named df.
df <- data.frame(days, temp, rain)
#Display of the data frame.
#   days temp  rain
# 1   Mon   78  TRUE
# 2  Tues   72  TRUE
# 3  Weds   60  TRUE
# 4 Thurs   55 FALSE
# 5   Fri   77 FALSE
```
We can run `str()` which will give us the structure of the data frame.
```r
str(df)
#Output.
# 'data.frame':	5 obs. of  3 variables:
#  $ days: chr  "Mon" "Tues" "Weds" "Thurs" ...
#  $ temp: num  78 72 60 55 77
#  $ rain: logi  TRUE TRUE TRUE FALSE FALSE
```
## Data frames: Selection and Indexing

With data frames we can organize data by values. We also can return data frames by index. Here is the data frame syntax: `dataFrameName[rows,cols]`. Below are two examples how to return rows and columns.
```r
#Returns all contents in first row.
df[1, ]
#Returns all items in the first column
df[ ,1] 
```

We can return column names.
```r
#Returns everything in the rain column.
df[ ,"rain"]
#Returns all five rows and all column values in temp and days.
df[1:5, c('days','temp')]
# > df[1:5, c('days','temp')]
#    days temp
# 1   Mon   78
# 2  Tues   72
# 3  Weds   60
# 4 Thurs   55
5   Fri   77

#Returns all the items in the days' column. Returns as a vector.
df$days
# > df$days
# [1] "Mon"   "Tues"  "Weds"  "Thurs" "Fri"  

#Returns the same as above BUT returns in a data frame format.
df['days']
# > df['days']
#    days
# 1   Mon
# 2  Tues
# 3  Weds
# 4 Thurs
# 5   Fri
```

Using subsets is a great way to return data that is passing a certain parameter: 
```r
#Grab the days where it doesn't rain (TRUE). We'll get a data frame where the values of rain are true.
subset(df, subset = rain == TRUE)
#syntax subset(dataframe, column arg value)
subset(df, subset = temp >= 78)

#Output:
# > subset(df, subset = rain == TRUE)
#   days temp rain
# 1  Mon   78 TRUE
# 2 Tues   72 TRUE
# 3 Weds   60 TRUE
# > subset(df, subset = temp >= 78)
#   days temp rain
# 1  Mon   78 TRUE
``` 
Using order will order the data frame by a certain value. Here is an example of using the `df` data frame and ordering it by the values in `temp`.
```r
sortedTemp <- order(df['temp'])
#Return sorted temps by index.
sortedTemp
# > sortedTemp
# [1] 4 3 2 5 1

#Using the sorted temp to have least temp to greatest temp by row number.
df[sortedTemp, ]
# > df[sortedTemp, ]
#    days temp  rain
# 4 Thurs   55 FALSE
# 3  Weds   60  TRUE
# 2  Tues   72  TRUE
# 5   Fri   77 FALSE
# 1   Mon   78  TRUE
```