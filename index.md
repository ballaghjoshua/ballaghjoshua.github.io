**GITHUB PAGE**  
https://ballaghjoshua.github.io/

# Final Tutorial: Public Education and Policy in Louisiana
<center>--- CMPS-3160 ---</center>
<center>--- Tulane University --- </center>
<center>--- By Josh Ballagh and Ellen Waller ---</center>
<center>--- Fall 2020 ---</center>

## Introduction
**Disclaimer: This page is still under construction!**  
We will be making major updates/overhauls as the semester progresses. This is simply our current working version.  
The final version will be available 11/24/2020.  
  
See the assignment project on the course webpage here: https://nmattei.github.io/cmps3160/projects/FinalTutorial/

For the final tutorial, we (Josh Ballagh and Ellen Waller) aim to examine a series of data sets that pertain to public education in Louisiana. Specifically, we will be looking at ACT results and graduation rates in Louisiana from 2005 to 2019. These academic markers are traditionally used to measure student and school performance, and they will be valuable in comparing the qualities of education that are available to children in different parishes and with different backgrounds. 

When viewed at the aggregate level, this data tells a story of Louisiana education as a whole, providing overall average test scores and graduation rates. This, however, is not the entire story. To get a clearer picture of the state of Louisiana’s public education, it will be essential to look at how these academic markers differ across parishes, as well as how these markers vary across specific subgroups (minority students, students with disabilities, and economically disadvantaged students). Breaking down the data along these lines will give us the ability to answer key questions: Which parishes have the highest academic performance? Which ones have the lowest? Which have experienced the most growth in the past decade, and which have declined? Do the highest performing parishes also have the highest performing subgroups? Is an upwards trend of academic performance overall in the state caused by the improvement of all parishes, or just a select few either at the top or bottom end of the distribution? Are specific subgroups experiencing the same overall trends of the parish and state? If so, which subgroups? Which parishes are doing a better job setting up the success of these subgroups, and how does this correlate to funding? With this data broken down to the parish level, we will then also be able to analyze the data in the context of the parish itself. We can compare the academic markers to the parish demographics, indicators of wealth, average levels of parent education, and employment rates, ultimately looking at which factors may or may not correlate.

As we look at this data, it will be important to keep in mind policy changes that have impacted Louisiana’s public education system in the past decade. In 2012, Louisiana pushed a statewide initiative for major education reform that resulted in three acts being signed into law: the Talent Statute (allowing schools to base personnel decisions more greatly on teacher effectiveness), the Choice Law (allowing for greater parent/student choice in the educational process), and the Early Childhood Education Act (establishing stronger foundations for students in early childhood). With data both preceding and succeeding the establishment of this initiative, we can look at whether or not these reforms have had an impact on high school performance, and in what areas. Furthermore, in 2015, the Every Student Succeeds Act (ESSA) was passed into law by the US Federal Government, allowing states more independence in determining the standards that students are held to. It also requires a multiple-measure accountability system for each state, and requires that all schools provide college/career counseling and advanced placement courses for all students. What, if any, impact has this major shift in education policy had on the state of Louisiana?

We hope to tackle these questions and more!


## Data Extraction
Our project will rely primarily on data published by the Louisiana Department of Education. For our first milestone, we have uploaded and tidied a dataset of primary and secondary school performance metrics in 2019 as published on the state's website here: https://louisianabelieves.com/resources/library/data-center  
  
This briefing from the state helps provide further context to the dataset: https://www.louisianabelieves.com/docs/default-source/data-management/2018-2019-school-and-center-performance-briefing.pdf?sfvrsn=4829a1f_4  
  
Now, let's load that data!

#### Import Libraries
So far, all we've needed to use for this project is the pandas library for creating dataframes. If we use any others, we'll list them out here!


```python
import pandas as pd
# we will likely need to import other stuff later!
```

#### Loading Excel Data
The LA Department of Education stored this data in an Excel file, split across three sheets by class: School, Alternative School, and Closed School. Lucky for us, pandas can easily read Excel files into dataframes! We'll just have to do some simple operations to tidy up our dataframe before we can use it.


```python
performance2019_df = pd.read_excel('2019-school-performance-scores.xlsx')
performance2019_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Unnamed: 1</th>
      <th>Unnamed: 2</th>
      <th>Unnamed: 3</th>
      <th>Unnamed: 4</th>
      <th>Unnamed: 5</th>
      <th>Unnamed: 6</th>
      <th>Unnamed: 7</th>
      <th>Unnamed: 8</th>
      <th>Unnamed: 9</th>
      <th>...</th>
      <th>Unnamed: 34</th>
      <th>Unnamed: 35</th>
      <th>Unnamed: 36</th>
      <th>Unnamed: 37</th>
      <th>Unnamed: 38</th>
      <th>Unnamed: 39</th>
      <th>Unnamed: 40</th>
      <th>Unnamed: 41</th>
      <th>Unnamed: 42</th>
      <th>Unnamed: 43</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019 School Performance Scores and Letter Grades</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Updated 2/12/2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2019 Letter Grade Equivalents for Key Indices</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Site Code</td>
      <td>School</td>
      <td>School System</td>
      <td>School Type                                (El...</td>
      <td>2019 Letter Grade</td>
      <td>2019 SPS</td>
      <td>2018 Letter Grade</td>
      <td>2018 SPS</td>
      <td>2019 K8 &amp; High School Assessment Letter Grade ...</td>
      <td>2019 K8 &amp; High School Progress Letter Grade Eq...</td>
      <td>...</td>
      <td>2018 K8 &amp; High School \nProgress Index</td>
      <td>2018 K8 Assessment Index</td>
      <td>2018 K8 Progress Index</td>
      <td>2018 Dropout Credit Accumulation Index</td>
      <td>2018 High School Assessment Index</td>
      <td>2018 High School Progress Index</td>
      <td>2018 ACT Index</td>
      <td>Strength of Diploma (Graduation Index) (2016-2...</td>
      <td>Cohort Graduation Rate Index  (Points Earned f...</td>
      <td>Cohort Graduation Rate (Actual Graduation Rate...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>001001</td>
      <td>Armstrong Middle School</td>
      <td>Acadia Parish</td>
      <td>Elementary/Middle School</td>
      <td>C</td>
      <td>61.8</td>
      <td>D</td>
      <td>53.7</td>
      <td>D</td>
      <td>C</td>
      <td>...</td>
      <td>67.5</td>
      <td>43.6</td>
      <td>67.5</td>
      <td>126.3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>001002</td>
      <td>Branch Elementary School</td>
      <td>Acadia Parish</td>
      <td>Elementary/Middle School</td>
      <td>A</td>
      <td>92</td>
      <td>B</td>
      <td>87.8</td>
      <td>B</td>
      <td>A</td>
      <td>...</td>
      <td>101.7</td>
      <td>79.6</td>
      <td>101.7</td>
      <td>133.8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 44 columns</p>
</div>



#### Tidying Up  
If you take a look at the first few rows of the dataframe as it was loaded, you'll likely notice a couple of problems: 1) that all 43 of its columns are unnamed and 2) that the first two rows of the dataframe are filled with NaN's, while the column names are hiding as values in Row 2. Below we'll run some code that fixes these issues!


```python
performance2019_df.columns = performance2019_df.loc[2] # Assign our columns names, pulling them from Row 2
performance2019_df = performance2019_df[3:1270] # cut off the rows at top and bottom filled with NaN's and non-values
performance2019_df.rename(columns = {'2019 Letter Grade ': '2019 Letter Grade', '2019 SPS ' : '2019 SPS', '2018 Letter Grade ': '2018 Letter Grade', '2018 SPS ':'2018 SPS'}, errors = 'raise', inplace = True) #some of these column names have annoying whitespace tacked on - let's fix that
```


```python
performance2019_df.reset_index(drop = True, inplace = True) # reset the index for convenience
performance2019_df # And let's see our beautiful, tidied-up table!
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>2</th>
      <th>Site Code</th>
      <th>School</th>
      <th>School System</th>
      <th>School Type                                (Elementary, Middle, High, Combination)</th>
      <th>2019 Letter Grade</th>
      <th>2019 SPS</th>
      <th>2018 Letter Grade</th>
      <th>2018 SPS</th>
      <th>2019 K8 &amp; High School Assessment Letter Grade Equivalent</th>
      <th>2019 K8 &amp; High School Progress Letter Grade Equivalent</th>
      <th>...</th>
      <th>2018 K8 &amp; High School \nProgress Index</th>
      <th>2018 K8 Assessment Index</th>
      <th>2018 K8 Progress Index</th>
      <th>2018 Dropout Credit Accumulation Index</th>
      <th>2018 High School Assessment Index</th>
      <th>2018 High School Progress Index</th>
      <th>2018 ACT Index</th>
      <th>Strength of Diploma (Graduation Index) (2016-2017 Cohort)</th>
      <th>Cohort Graduation Rate Index  (Points Earned for Cohort Graduation Rate) (2016-2017  Cohort)</th>
      <th>Cohort Graduation Rate (Actual Graduation Rate) (2016-2017 Cohort)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>001001</td>
      <td>Armstrong Middle School</td>
      <td>Acadia Parish</td>
      <td>Elementary/Middle School</td>
      <td>C</td>
      <td>61.8</td>
      <td>D</td>
      <td>53.7</td>
      <td>D</td>
      <td>C</td>
      <td>...</td>
      <td>67.5</td>
      <td>43.6</td>
      <td>67.5</td>
      <td>126.3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>001002</td>
      <td>Branch Elementary School</td>
      <td>Acadia Parish</td>
      <td>Elementary/Middle School</td>
      <td>A</td>
      <td>92</td>
      <td>B</td>
      <td>87.8</td>
      <td>B</td>
      <td>A</td>
      <td>...</td>
      <td>101.7</td>
      <td>79.6</td>
      <td>101.7</td>
      <td>133.8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>001003</td>
      <td>Central Rayne Kindergarten School</td>
      <td>Acadia Parish</td>
      <td>Elementary/Middle School</td>
      <td>C</td>
      <td>68.5</td>
      <td>C</td>
      <td>73.9</td>
      <td>D</td>
      <td>A</td>
      <td>...</td>
      <td>102.9</td>
      <td>64.2</td>
      <td>102.9</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>001004</td>
      <td>Church Point Elementary School</td>
      <td>Acadia Parish</td>
      <td>Elementary/Middle School</td>
      <td>C</td>
      <td>61.9</td>
      <td>C</td>
      <td>63.7</td>
      <td>D</td>
      <td>B</td>
      <td>...</td>
      <td>77.6</td>
      <td>59</td>
      <td>77.6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>001005</td>
      <td>Church Point High School</td>
      <td>Acadia Parish</td>
      <td>High School</td>
      <td>B</td>
      <td>77.1</td>
      <td>B</td>
      <td>80.7</td>
      <td>D</td>
      <td>C</td>
      <td>...</td>
      <td>71.8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>62.9</td>
      <td>71.8</td>
      <td>62.1</td>
      <td>93.9</td>
      <td>99.4</td>
      <td>89.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1262</th>
      <td>WBR001</td>
      <td>Athlos Academy of Jefferson Parish</td>
      <td>Athlos Academy of Jefferson Parish</td>
      <td>Elementary/Middle School</td>
      <td>F</td>
      <td>43.6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
      <td>D</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1263</th>
      <td>WBU001</td>
      <td>Rosenwald Collegiate Academy</td>
      <td>Orleans Parish</td>
      <td>High School</td>
      <td>B</td>
      <td>84.5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C</td>
      <td>A</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1264</th>
      <td>WBV001</td>
      <td>Dwight D. Eisenhower Charter School</td>
      <td>Orleans Parish</td>
      <td>Elementary/Middle School</td>
      <td>C</td>
      <td>63.8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
      <td>A</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1265</th>
      <td>WJ5001</td>
      <td>Collegiate Baton Rouge</td>
      <td>Collegiate Baton Rouge</td>
      <td>High School</td>
      <td>C</td>
      <td>64.1</td>
      <td>C</td>
      <td>64.4</td>
      <td>F</td>
      <td>A</td>
      <td>...</td>
      <td>82.9</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.9</td>
      <td>82.9</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1266</th>
      <td>WZ8001</td>
      <td>GEO Prep Mid-City of Greater Baton Rouge</td>
      <td>GEO Prep Mid-City of Greater Baton Rouge</td>
      <td>Elementary/Middle School</td>
      <td>T</td>
      <td>56</td>
      <td>T</td>
      <td>51</td>
      <td>F</td>
      <td>A</td>
      <td>...</td>
      <td>92.2</td>
      <td>30.4</td>
      <td>92.2</td>
      <td>134.2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1267 rows × 44 columns</p>
</div>



#### Bonus Round
Let's see 2019 data on where Josh went to high school, the Louisiana School for Math, Science, and the Arts!


```python

```


```python
lsmsa_data = performance2019_df.set_index("School").loc[
    "Louisiana School for Math Science & the Arts"]  # Grab LSMSA's data
mean_SPS = performance2019_df['2019 SPS'].astype('float64').mean()
max_SPS = performance2019_df['2019 SPS'].astype('float64').max()

print("The state's mean SPS was", mean_SPS,
      "in 2019. LSMSA's SPS that year was", lsmsa_data['2019 SPS'])
print("The max SPS was", max_SPS, "in 2019. I wonder who got that score?")

bf_data = performance2019_df.set_index(
    "School").loc["Benjamin Franklin High School"]
print(
    "It appears to be our old rivals, Benjamin Franklin in Baton Rouge. Their 2019 SPS was",
    bf_data['2019 SPS'])
```

    The state's mean SPS was 73.65982636148384 in 2019. LSMSA's SPS that year was 127.1
    The max SPS was 135.5 in 2019. I wonder who got that score?
    It appears to be our old rivals, Benjamin Franklin in Baton Rouge. Their 2019 SPS was 135.5



```python

```
