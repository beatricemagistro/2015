# Lab 1: Introduction to R and RStudio, and knitr
Jeffrey B. Arnold and Carolina Johnson  
April 3, 2015  





# Learning Objectives

1. Install R and RStudio
2. Load data from a csv into R



# Installing R

Install R, RStudio and **devtools**.
Follow the instructions [here](http://UW-POLS503.github.io/pols_503_sp15/getting_help_with_r.html).



# Orientation with RStudio

R is the name of the programming language, and RStudio is a convenient and widely used interface to that language.

Since you will be using it for the remainder of the course, you should familiarize yourself with the RStudio GUI.

![RStudio GUI](./images/RStudio.png)

It consists of four windows,

1. Bottom left: The **console** window. You type commands at the ``>`` prompt and R executes them.
2. Top left: The **editor** window. Here you can edit and save R scripts which contain multiple R commands.
    - You can open a new R script using *File -> New -> R script*.
    - If you highlight an area, you can run those commands in the console with the "Run" button.
    - You can run all the commands in the **editor** window using the "Source" button.
3. Top right
    - **workspace** lists all R objects (variables) that are defined
    - **history** lists all the commands that have been typed into the console.
4. Bottom right

    - **files** allows you to browse directories and open files.
    - **plots** displays any plots created. In this window you can toggle back through previously created plots.
    - **packages** shows which packages are installed and loaded.
    - **help** displays R help.

RStudio documentation can be found at <http://www.rstudio.com/ide/docs/>.
Of those, the most likely to be useful to you are:

- [Working in the Console](http://www.rstudio.com/ide/docs/using/console)
- [Editing and Executing Code](http://www.rstudio.com/ide/docs/using/source)
- [Viewing Command History](http://www.rstudio.com/ide/docs/using/history)

**Challenge:**

1. Go to *Tools > Global Options*. Change the font and color of the editor and console. Which one do you like the best?
2. What happens when you type `Alt+Shift+K`?


# Using R as a calculator

Although it is so much more, you can use R as a calculator.
For example, to add, subtract, multiply or divide:

```r
2 + 3
2 - 3
2 * 3
2 / 3
```

The power of a number is calculated with ``^``, e.g. $4^2$ is,


```r
4 ^ 2
```

R includes many functions for standard math functions.
For example, the square root function is ``sqrt``, e.g. $\sqrt{2}$,


```r
sqrt(2)
```

And you can combine many of them together

```r
(2 * 4 + 3 ) / 10
sqrt(2 * 2)
```



# Variables and Assignment

In R, you can save the results of calculations into objects that you can use later.
This is done using the special symbol, ``<-``.
For example, this saves the results of 2 + 2 to an object named ``foo`` [^1]

```r
foo <- 2 + 2
```
You can see that ``foo`` is equal to ``4``

```r
foo
```
And you can reuse foo in other calculations,

```r
foo + 3
foo / 2 * 8 + foo
```

[^1]: If you are curious as to why the variable was named `foo`, read [this](http://en.wikipedia.org/wiki/Foobar).

You can use `=` instead of `<-` for assignment.
You may see this in some other code.
There are some technical reasons to use `<-` instead of `=`, but the primary reason we will use `<-` instead of `=` is that this is the convention used in modern `R` programs.

**Challenge**
1. Create a variable named whatever strikes your fancy and set it equal to the square root of 2.
Then multiply it by 4.
2. Create a variable with a really long name and assign it a value. Start typing its name
3. Enter the following in the console `sdgagasdgjasda`.


# Working Directory and R Projects

## Working Directory


## R Projects

Keeping all the files associated with a project organized together – input data, R scripts, analytical results, figures – is such a wise and common practice that RStudio has built-in support for this via its projects.  Read [this](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects) for more information about RStudio projects.

You will use RStudio projects for your labs and homeworks, and **final paper**.
Create a RStudio project that you will use for all your labs.

1. *File -> New Project*
2. Select "New Directory"
3. Select "Empty Project"
4. Select a name for your project as Directory Name.
   "POLS_503_Labs" is as good as any, and better than most.
   Then choose where to put this directory with "Create project as sub-directory of".
   Don't worry about the other options.



# Creating your first R Markdown Document

For this course, you will be we using R Markdown documents for homeworks.
Create your firs

1. *File -> New File -> R Markdown*
2. Choose a title and author for your file.  HTML output is fine.
3. Hit OK. This will open a template for your Markdown file.
4. Save this file with `Ctrl-S`.
5. Click on the "Knit HTML" button. This will create a HTML document from this
   document.


Cheatsheets and additional resources about R Markdown are available at <http://rmarkdown.rstudio.com/>.


# Loading Data into R

For the remainder of this lab you will be using a dataset of GDP per capita and fertility
from Gapminder.[^2]

[^2]: Dataset from the [gapminder](https://github.com/jennybc/gapminder) R packager.
      The dataset in that package is an excerpt from the [Gapminder](http://www.gapminder.org/data/) data. Gapminder data is released under the Creative Commons Attribution 3.0 Unported license. See their [terms of use](https://docs.google.com/document/pub?id=1POd-pBMc5vDXAmxrpGjPLaCSDSWuxX6FLQgq5DhlUhM).


Download the csv ("[comma-separated values](http://en.wikipedia.org/wiki/Comma-separated_values)")" <https://github.com/POLS503/pols_503_sp15/blob/master/labs/gapminder.csv>.

Then load the file


```r
gapminder <- read.csv("gapminder.csv", stringsAsFactors = FALSE)
```

This creates a *data frame*.
A *data frame* is a type of R object that corresponds to what you usually think of as a dataset or a spreadsheet --- rows are observations and columns are variables.

**Challenge:**
What happens when you do the following?

```r
gapminder
```

This is a lot of information. How can we get a more useful picture of the dataset as a whole?


```r
dim(gapminder)
names(gapminder)
head(gapminder)
summary(gapminder)
```

- `dim` shows the dimensions of the data frame as the number of rows, columns
- `names` shows the column names of the data frame.
- `head` shows the first few observations
- `summary` calculates summary statistics for all variables in the data frame.

**Challenge:** Given the information previously:

1. What are the variables in the dataset?
2. How many observations are there?
3. What is the unit of observation?
3. What types of data are the different variables?
4. What is the range of years in the data?
5. What are the mean and median life expectancy?

# Working with variables in Data Frames

You can extract single variables (or columns) and perform different operations on them.
To extract a variable, we use the dollar sign (`$`) extraction operator.

```r
gapminder$lifeExp
```

Again, perhaps a summary may be more interesting. We can do more specific operations on this variable alone:


```r
mean(gapminder$lifeExp)
median(gapminder$lifeExp)
sd(gapminder$lifeExp)
min(gapminder$lifeExp)
max(gapminder$lifeExp)
quantile(gapminder$lifeExp)
```

**Challenge**
1. What are the mean and median of GDP per capita?
2. Find the 30th percentile of GDP per capita?
3. The function `length()` calculates the length of a vector.
   The function `unique()` returns the number of unique values in a vector.
   How many countries in the data are there? How many years?

# Distributions

Summary statistics reduce the information of a distribution to single values.
A distribution providess a richer understanding of the data.
Look at the distribution of the variable `lifeExp`.

You will use the **ggplot2** package for graphics for most of this course.
In order to use it, you will need to load it using `library()`

```r
library("ggplot2")
```

Create a histogram:

```r
ggplot(gapminder, aes(x = lifeExp)) +
  geom_histogram()
```

You could also save the plot to a variable

```r
lifexp_plot <- ggplot(gapminder, aes(x = lifeExp)) +
                      geom_histogram()
```

If you just enter the variable name in the console it will "print"" the object, which in this case, simply creates the plot:

```r
lifexp_plot
```

**Challenge** Explore another variable of your choosing

1. Look at some summary statistics for that variable.
2. Visualize the distribution of that variable with a histogram.
3. Describe this distribution in plain ordinary English to your partner.
4. Write it as discussion in your R Markdown file.



# Exploring relationships between variables

Use **ggplot** to create hisograms for each year

```r
lifexp_plot + facet_wrap( ~ continent)
```

**Challege:**
Describe how the distribution varies across years (Write it in your Markdown!)

You can also use **ggplot2** to create a scatterplot

```r
ggplot(gapminder, aes(y = lifeExp, x = log(gdpPercap))) +
  geom_point() +
  geom_smooth()
```

**Challenge:**

1. Why is GDP per capita logged?
2. Create a plot with a scatter plot of life expectancy vs. GDP per capita for each year.


# Comments

Any R code following a hash (``#``) is not executed.
These are called comments, and can and **should** be used to annotate and explain your code.
For example, this doesn't do anything.

```r
#thisisacomment
```
And in this, nothing after the ``#`` is executed,

```r
#this is still a comment
2 + 2 # this is also a comment
```

**Challenge:**
What is this equal to?

```r
5 * 4 # + 3 # - 8
```

# R Scripts

You can save R commands in a file called an R script.
To create a new R Script use *File -> New File -> R Script*.
This will create a new tab in the upper left panel which will have a name like "Untitled1".
Save this to a file with the extension ".R" (RStudio will warn you if you do not)

To see how this works, write a few commands in the editor.
For example,

```r
2 + 2
3 + 8
mean(c(1, 2, 3))
```
You can run the current line or highlighted section with *Ctl-Enter* or the *Run* button.

# Getting Help with R

Refer to [Getting Help with R](http://UW-POLS503.github.io/pols_503_sp15/getting_help_with_r.html)

1. Refer to http://docs.ggplot2.org/current/ to find out how to create a density plot. Create a density plot of `gdpPercap`. Is is right skewed, left skewed, or symmetric?
2. Go to stackoverlow and search for questions with tag `[r]`.

    * What are featured questions today?
    * What is the most voted on question?
	  * What is in the info tab?

3. Find and download the **cowsay** package. You cannot use `install.packages`. What does the `cowsay` function do? Run it with something fun (it'll make make sense once you know what it does).

* * *

Some text and the data set used in this are taken from Jenny Bryant, [R basics, workspace and working directory, RStudio projects](https://stat545-ubc.github.io/block002_hello-r-workspace-wd-project.html), licensed under [CC BY-NC 3.0](http://creativecommons.org/licenses/by-nc/3.0/)


* * *



