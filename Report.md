# Programming for Data Science Report 


## a. List all of countries in the dataset

![Functionality a](https://github.com/ACV1904/Programming/figures/Figure-a.png)

## b. Describe any problem with the data including missing data, data format etc.

Given the importance of the number of suicides for this dataset, I did notice that the number of non-null values in that column was lower than the values in other columns. I also found that the type of the values in that column was an object when we would expect an integer or a float. The same occurs with the column “ gdp_for_year ($)” where the numbers show commas, so they’re not integers, and the name shows a blank space at the beginning which could be confusing later. These issues would need to be sorted.

<img src= "Programming/figures/Figure-b-1.png" width="450">
<img src= "Programming/figures/Figure-b-2.png" width="400">

## c. Clean and transform the data into the correct data types

This part is carried out in different parts of the code, given that some problems appeared when working in other functions. Data cleaning:
1. Checked the number of duplicates, and found 20, so dropped those rows. (number of rows: 27,820)
2. Changed the value type of the “suicides_no” column from object to number. Then the number of null values in this column was 4281, so I dropped these rows, in another data frame: df2 (number of rows: 23,539). It’s still a good number to work with.


## d. Add a new column “suicides/100k” and generate its data

![Functionality d](https://github.com/ACV1904/Programming/figures/Figure-d.png)


## e. Add a new column “generation” and fill up its data according to below criteria

| Value 	 | Criteria 		    |
|Lost Generation | born between 1883 - 1900 |
|G.I. Generation | born between 1901 - 1927 |
|Silent          | born between 1928 - 1945 |
|Boomers         | born between 1946 – 1964 |
|Generation X    | born between 1965 - 1980 |
|Millennials     | born between 1981 - 1995 |
|Generation Z    | born between 1996 – 2010 |
|Generation A    | born between 2011 – 2025 |

First, I got the first number of the column age. Then I subtracted this number to the column year, to get the first year of the generation, and assigned it to a new column. 
- Then, I created a function to assign a generation name to the ranges of years.  
- Finally, I used ‘apply’ to get the generation from the new years I got before. And this, I assigned it to a new column “Generation”.

<img src= "Programming/figures/Figure-e-2.png" width="450">

## f. Add a new column “gdp_per_capita” and fill its data. GDP per Capita of a country is GDP divided by population of that country.

- First, I performed a ‘groupby’ with ‘transform(sum)’ to the first data frame (before dropping the null values in the column suicide_no), to get the total population by year of each country.
- Then, I did the data cleaning of the column with the data of the GDP per year
- Finally, because the data of population and GDP are already per year, I divided the GDP by the population and put it in the new column “GDP_per_capita”

<img src= "Programming/figures/Figure-f-1.png" width="450">
<img src= "Programming/figures/Figure-f-2.png" width="450">

## g. Rank countries by total suicides

- With the given data, I performed a ‘groupby’ with ‘sum’, to get all the suicides per country.
- Then sorted it in descending order to see the countries with the highest number first.
I haven’t check that all countries in the data set have the information for the same years, or if they have data for all the years.

<img src= "Programming/figures/Figure-g.png" width="400">

## h. Given a country name, find the year that had the highest number of suicides

- Created a new data frame with the columns of the country, the year and the number of suicides per year.
- Defined a function that received a country name and found the year with the highest number of suicides for that country.
- Finally, I called the function in a print line so see the result

<img src= "Programming/figures/Figure-h.png" width="450">

## i. Given a year and country name, calculate the number of suicides by gender

- Similarly to the previous section, I created a new data frame with the columns of the country, year, sex and the number of suicides per gender. 
- Then, I created a new data frame with the data of the previous data frame, but showing only the rows of the country and year given. So, we can see the number of suicides for males and females.

<img src= "Programming/figures/Figure-i.png" width="450">

## j. Find total suicides by continents

- First, I searched online for a data set of countries with their continents. I imported the file as another data frame.
- Then, I made a left merge between the main data frame and the new one (on ‘country’) and saved it as a new data frame. During his process, some problems appeared.  I checked this by counting the number of null values I got in the new column “Continent”. Then checking the countries in the rows with empty “Continent” values.

- Because there were problems with 8 countries, I checked country by country. Five of those countries were present in the list of continents but with another name, so I replaced them. The other 3 countries were not present, so I had to input them manually. I created a dictionary with this, assigned it to another data frame and then concatenated it with the continents data frame. 
- With this sorted, I could perform a ‘groupby’ and ‘sum’ to get the total number of suicides per continent.

<img src= "Programming/figures/Figure-j-1.png" width="400">
<img src= "Programming/figures/Figure-j-2.png" width="400">

## k. Find correlations between suicides, GDP per capita and population. What are your conclusions?

![Functionality k](https://github.com/ACV1904/Programming/figures/Figure-k-0.png)

- First, I created a data frame with the features required for the correlation analysis: I grouped them by GDP_per_capita and total_pop, and added the number of suicides. Because this created a dataframe with 2 columns of indexes, I had to reset the index.
- I installed the necessary libraries
- I performed the correlation function to the last data frame. Then plot the heatmap, and show the matrix:

![Correlation heatmap](https://github.com/ACV1904/Programming/figures/Figure-k-1.png)

-	With the heatmap is easier to see that there is a positive correlation between the number of suicides and the size of the population (the coefficient of Pearson is 0.8, close to 1). It means that if the population increases, the suicides increase. 
-	The Pearson coefficient between the GDP per capita and the number of suicides is closer to 0, so there is no clear correlation between those features. The same happens with the correlation between the GDP per capita and the size of the population.


## l. Use appropriate visual notation to visualise total suicides over years. Describe your arguments

<img src= "Programming/figures/Figure-l-0.png" width="450">

Like in the previous section, I created a data frame with the data of number of suicides grouped by years. With these I did a line chart.

![Line chart of suicides over the years](https://github.com/ACV1904/Programming/figures/Figure-l-1.png)

From the graph we can clearly see the number of suicides is increasing over the years until 1994, then it varies reasonably, until the last year in which it drops considerably. Checking the data from the last 2 years its clear that there must be a good proportion of data from 2016 that is missing, so that year is not representative.

## m. Compare suicides by gender over years and state your conclusions

<img src= "Programming/figures/Figure-m-0.png" width="450">

- Again, I created a new data frame with the data needed, but I dropped the data from 2016, because it wasn’t reliable.
- Then I needed the list of values for females, males, and the list of years for the x axis.
- With these lists I generated a line chart:

![Line chart of suicides per gender over the years](https://github.com/ACV1904/Programming/figures/Figure-m-1.png)

The graph allows to visualize that the number of suicides by males is considerably higher than the one of females.

## n. Calculate and Visualise suicides on generation and on age group. Describe your findings

After creating a new data frame with the required data, I found online a method to draw a stacked bar plot. Here I created a dictionary with the age ranges as keys and the number of suicides per generation as values.

![Stacked bar plot: suicides per generation and age range](https://github.com/ACV1904/Programming/figures/Figure-n-1.png)

From this graph its visible how the number of suicides in our dataset increases by generation until Generation X and then decreases again. This is not only related to the nature of the suicides, but to the years the samples were taken as well. It also looks like most cases are in the ranges of 35-54 years and 55-74 years. It may be confusing to say that the number of suicides of younger people increases over time, but it also has to do with the years the sample were taken. From these records no suicide of younger people belonged to Boomers for instance. And no people from the G.I. Generation was younger than 75.



## Reflection

The program was developed following the lectures and tutorials, as well as searching online for the pandas’ documentation and other websites (stackoverflow.com among others). 
I think, given more time, I could have explored the data better, to have a better understanding of the null values in the main feature of this dataset, the number of suicides. I believe there is some data missing in which the totals of gender, age or GDP might be affected by, but I don’t think this was significant for the present analysis. I was careful to consider the population values from the original dataset. 
The time constraint was another reason to skip the analysis of the method in which the data was created. It would allow me to have a better understanding of it, and better judging for the manipulation of the data.
Working on Jupyter notebook was easier to run the code by segments, but I had to be careful of the parts of the code I was running. For some functions I had to run the whole code, to make sure I don’t get errors. I also realized that when working on Google Colab Notebook was necessary to load the data every time I came back to the code. I downloaded the file and worked on it on PyCharm. In PyCharm I had to install the libraries when I closed and opened the file as well. I feel I still need to familiarize myself with the programs, but I think I got the idea of what I could do.
December 2023  
