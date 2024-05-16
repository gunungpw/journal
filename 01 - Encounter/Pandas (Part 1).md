In the NumPy section we dealt with some arrays, whose columns had each a special meaning. For example, the column number 0 could contain values interpreted as years, and column 1 could contain a month, and so on. It is possible to handle the data this way, but it can be hard to remember, which column number corresponds to which variable. Especially, if you later remove some column from the array, then the numbering of the remaining columns changes. One solution to this is to give a descriptive name to each column. These column names stay fixed and attached to their corresponding columns, even if we remove some of the columns. In addition, the rows can be given names as well, these are called _indices_ in Pandas.

The [Pandas](http://pandas.pydata.org/) library is built on top of the NumPy library, and it provides a special kind of two dimensional data structure called `DataFrame`. The `DataFrame` allows to give names to the columns, so that one can access a column using its name in place of the index of the column.

First we will quickly go through a few examples to see what is possible with Pandas. You may need to check some details from the Pandas [documentation](http://pandas.pydata.org/pandas-docs/stable/) in order to complete the exercises. We start by doing some standard imports:

```capnproto
import pandas as pd    # This is the standard way of importing the Pandas library
import numpy as np
```

Let's import some weather data that is in text form in a csv (Comma Separated Values) file. The following call will fetch the data from the internet and convert it to a DataFrame:

```makefile
wh = pd.read_csv("https://raw.githubusercontent.com/csmastersUH/data_analysis_with_python_2020/master/kumpula-weather-2017.csv")
wh.head()   # The head method prints the first 5 rows
```

||Year|m|d|Time|Time zone|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|UTC|-1.0|-1.0|0.6|
|1|2017|1|2|00:00|UTC|4.4|-1.0|-3.9|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|
|3|2017|1|4|00:00|UTC|-1.0|13.0|-12.8|
|4|2017|1|5|00:00|UTC|-1.0|10.0|-17.8|

We see that the DataFrame contains eight columns, three of which are actual measured variables. Now we can refer to a column by its name:

```bash
wh["Snow depth (cm)"].head()     # Using the tab key can help enter long column names
```

`0 -1.0   1 -1.0   2 7.0   3 13.0   4 10.0   Name: Snow depth (cm), dtype: float64`

There are several summary statistic methods that operate on a column or on all the columns. The next example computes the mean of the temperatures over all rows of the DataFrame:

```stata
wh["Air temperature (degC)"].mean()    # Mean temperature
```

`6.5271232876712331`

We can drop some columns from the DataFrame with the `drop` method:

```sql
wh.drop("Time zone", axis=1).head()    # Return a copy with one column removed, the original DataFrame stays intact
```

||Year|m|d|Time|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|-1.0|-1.0|0.6|
|1|2017|1|2|00:00|4.4|-1.0|-3.9|
|2|2017|1|3|00:00|6.6|7.0|-6.5|
|3|2017|1|4|00:00|-1.0|13.0|-12.8|
|4|2017|1|5|00:00|-1.0|10.0|-17.8|

```cmake
wh.head()     # Original DataFrame is unchanged
```

||Year|m|d|Time|Time zone|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|UTC|-1.0|-1.0|0.6|
|1|2017|1|2|00:00|UTC|4.4|-1.0|-3.9|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|
|3|2017|1|4|00:00|UTC|-1.0|13.0|-12.8|
|4|2017|1|5|00:00|UTC|-1.0|10.0|-17.8|

In case you want to modify the original DataFrame, you can either assign the result to the original DataFrame, or use the `inplace` parameter of the `drop` method. Many of the modifying methods of the DataFrame have the `inplace` parameter.

Addition of a new column works like adding a new key-value pair to a dictionary:

```stata
wh["Rainy"] = wh["Precipitation amount (mm)"] > 5
wh.head()
```

||Year|m|d|Time|Time zone|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|Rainy|
|---|---|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|UTC|-1.0|-1.0|0.6|False|
|1|2017|1|2|00:00|UTC|4.4|-1.0|-3.9|False|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|True|
|3|2017|1|4|00:00|UTC|-1.0|13.0|-12.8|False|
|4|2017|1|5|00:00|UTC|-1.0|10.0|-17.8|False|

In the next sections we will systematically go through the DataFrame and its one-dimensional version: _Series_.

## Creation and indexing of series

One can turn any one-dimensional iterable into a Series, which is a one-dimensional data structure:

```apache
s=pd.Series([1, 4, 5, 2, 5, 2])
s
```

`0 1   1 4   2 5   3 2   4 5   5 2   dtype: int64`

The data type of the elements in this Series is `int64`, integers representable in 64 bits.

We can also attach a name to this series:

```abnf
s.name = "Grades"
s
```

`0 1   1 4   2 5   3 2   4 5   5 2   Name: Grades, dtype: int64`

The common attributes of the series are the `name`, `dtype`, and `size`:

```python
print(f"Name: {s.name}, dtype: {s.dtype}, size: {s.size}")
```

`Name: Grades, dtype: int64, size: 6`

In addition to the values of the series, also the row indices were printed. All the accessing methods from NumPy arrays also work for the Series: indexing, slicing, masking and fancy indexing.

```apache
s[1]
```

`4`

```lua
s2=s[[0,5]]                    # Fancy indexing
print(s2)
```

`0 1   5 2   Name: Grades, dtype: int64`

```excel
t=s[-2:]                    # Slicing
t
```

`4 5   5 2   Name: Grades, dtype: int64`

Note that the indices stick to the corresponding values, they are not renumbered!

```apache
t[4]                        # t[0] would give an error
```

`5`

The values as a NumPy array are accessible via the `values` attribute:

```maxima
s2.values
```

`array([1, 2])`

And the indices are available through the `index` attribute:

```axapta
s2.index
```

`Int64Index([0, 5], dtype='int64')`

The index is not simply a NumPy array, but a data structure that allows fast access to the elements. The indices need not be integers, as the next example shows:

```apache
s3=pd.Series([1, 4, 5, 2, 5, 2], index=list("abcdef"))
s3
```

`a 1   b 4   c 5   d 2   e 5   f 2   dtype: int64`

```axapta
s3.index
```

`Index(['a', 'b', 'c', 'd', 'e', 'f'], dtype='object')`

```css
s3["b"]
```

`4`

```css
s3["b":"e"]
```

`b 4   c 5   d 2   e 5   dtype: int64`

It is still possible to access the series using NumPy style _implicit integer indices_:

```apache
s3[1]
```

`4`

This can be confusing though. Consider the following series:

```apache
s4 = pd.Series(["Jack", "Jones", "James"], index=[1,2,3])
s4
```

`1 Jack   2 Jones   3 James   dtype: object`

What do you think `s4[1]` will print? For this ambiguity Pandas offers attributes `loc` and `iloc`. The attributes `loc` always uses the explicit index, while the attribute `iloc` always uses the implicit integer index:

```stylus
print(s4.loc[1])
print(s4.iloc[1])
```

`Jack   Jones`

### Exercise 3.13 (read series)

Write function `read_series` that reads input lines from the user and return a Series. Each line should contain first the index and then the corresponding value, separated by whitespace. The index and values are strings (in this case `dtype` is `object`). An empty line signals the end of Series. Malformed input should cause an exception. An input line is malformed, if it is non-empty and, when split at whitespace, does not result in two parts.

Test your function from the `main` function.

### Exercise 3.14 (operations on series)

Write function `create_series` that gets two lists of numbers as parameters. Both lists should have length 3. The function should first create two Series, `s1` and `s2`. The first series should have values from the first parameter list and have corresponding indices `a`, `b`, and `c`. The second series should get its values from the second parameter list and have again the corresponding indices `a`, `b`, and `c`. The function should return the pair of these Series.

Then, write a function `modify_series` that gets two Series as parameters. It should add to the first Series `s1` a new value with index `d`. The new value should be the same as the value in Series `s2` with index `b`. Then delete the element from `s2` that has index `b`. Now the first Series should have four values, while the second list has only two values. Adding a new element to a Series can be achieved by assignment, like with dictionaries. Deletion of an element from a Series can be done with the `del` statement.

Test these functions from the main function. Try adding together the Series returned by the `modify_series` function. The operations on Series use the indices to keep the element-wise operations _aligned_. If for some index the operation could not be performed, the resulting value will be `NaN` (Not A Number).

### Exercise 3.15 (inverse series)

Write function `inverse_series` that get a Series as a parameter and returns a new series, whose indices and values have swapped roles. Test your function from the `main` function.

What happens if some value appears multiple times in the original Series? What happens if you use this value to index the resulting Series?

One may notice that there are similarities between Python's dictionaries and Pandas' Series, both can be thought to access values using keys. The difference is that Series requires that the indices have all the same type, and similarly, all the values have the same type. This restriction allows creation of fast data structures.

As a mark of the similaries between these two data structures, Pandas allows creation of a `Series` object from a dictionary:

```apache
d = { 2001 : "Bush", 2005: "Bush", 2009: "Obama", 2013: "Obama", 2017 : "Trump"}
s4 = pd.Series(d, name="Presidents")
s4
```

`2001 Bush   2005 Bush   2009 Obama   2013 Obama   2017 Trump   Name: Presidents, dtype: object`

## Summary (week 3)

- You found that comparisons are also vectorized operations, and that the result of a comparison can be used to mask (i.e. restrict) further operations on arrays
- You can select a list of columns using fancy indexing
- An application of NumPy arrays: basic linear algebra operations and solving systems of linear equations
- You know the building blocks of matplotlib's figures. You can create figures based on NumPy arrays and you can adjust the attributes of figures
- You understand how (raster) images are organized as NumPy arrays. You can manipulate images using Numpy's array operations.
- In Pandas it is standard to use rows of DataFrames as samples and columns as variables
- Both rows and columns of Pandas DataFrames can have names, i.e. indices
    
    - Operations maintain these indices even when adding or removing rows or columns
    - Indices also allow several operations to be combined meaningfully and easily

```elm
import pandas as pd
import numpy as np
```

## Creation of dataframes

The DataFrame is essentially a two dimensional object, and it can be created in three different ways:

- out of a two dimensional NumPy array
- out of given columns
- out of given rows

### Creating DataFrames from a NumPy array

In the following example a DataFrame with 2 rows and 3 column is created. The row and column indices are given explicitly.

```stylus
df=pd.DataFrame(np.random.randn(2,3), columns=["First", "Second", "Third"], index=["a", "b"])
df
```

||First|Second|Third|
|---|---|---|---|
|a|1.273012|-1.645268|0.133877|
|b|0.742194|-0.225893|2.600842|

Note that now both the rows and columns can be accessed using the special `Index` object:

```applescript
df.index                            # These are the "row names"
```

Index(['a', 'b'], dtype='object')

```applescript
df.columns                          # These are the "column names"
```

Index(['First', 'Second', 'Third'], dtype='object')

If either `columns` or `index` argument is left out, then an implicit integer index will be used:

```stylus
df2=pd.DataFrame(np.random.randn(2,3), index=["a", "b"])
df2
```

||0|1|2|
|---|---|---|---|
|a|0.095937|-0.688698|0.653831|
|b|0.978782|0.034069|1.125257|

Now the column index is an object similar to Python's builtin `range` type:

```excel
df2.columns
```

RangeIndex(start=0, stop=3, step=1)

### Creating DataFrames from columns

A column can be specified as a list, an NumPy array, or a Pandas' Series. The names of the columns can be given either with the `columns` parameter, or if Series objects are used, then the `name` attribute of each Series is used as the column name.

```apache
s1 = pd.Series([1,2,3])
s1
```

0    1
1    2
2    3
dtype: int64

```apache
s2 = pd.Series([4,5,6], name="b")
s2
```

0    4
1    5
2    6
Name: b, dtype: int64

Give the column name explicitly:

```stylus
pd.DataFrame(s1, columns=["a"])
```

||a|
|---|---|
|0|1|
|1|2|
|2|3|

Use the `name` attribute of Series s2 as the column name:

```armasm
pd.DataFrame(s2)
```

||b|
|---|---|
|0|4|
|1|5|
|2|6|

If using multiple columns, then they must be given as the dictionary, whose keys give the column names and values are the actual column content.

```armasm
pd.DataFrame({"a": s1, "b": s2})
```

||a|b|
|---|---|---|
|0|1|4|
|1|2|5|
|2|3|6|

### Creating DataFrames from rows

We can give a list of rows as a parameter to the DataFrame constructor. Each row is given as a dict, list, Series, or NumPy array. If we want to give names for the columns, then either the rows must be dictionaries, where the key is the column name and the values are the elements of the DataFrame on that row and column, or else the column names must be given explicitly. An example of this:

```apache
df=pd.DataFrame([{"Wage" : 1000, "Name" : "Jack", "Age" : 21}, {"Wage" : 1500, "Name" : "John", "Age" : 29}])
df
```

||Age|Name|Wage|
|---|---|---|---|
|0|21|Jack|1000|
|1|29|John|1500|

Or:

```prolog
df = pd.DataFrame([[1000, "Jack", 21], [1500, "John", 29]], columns=["Wage", "Name", "Age"])
df
```

||Wage|Name|Age|
|---|---|---|---|
|0|1000|Jack|21|
|1|1500|John|29|

In the earlier case, however, where we created DataFrames from a dictionary of columns, the order of columns should be the same as in the parameter dictionary in the recent versions of Python and Pandas.

In the sense of information content the order of columns should not matter, but sometimes you want to specify a certain order to make the Frame more readable, or to make it obey some semantic meaning of column order.

### 

Exercise 4.1 (cities)

Write function `cities` that returns the following DataFrame of top Finnish cities by population:

```apache
                 Population Total area
Helsinki         643272     715.48
Espoo            279044     528.03
Tampere          231853     689.59
Vantaa           223027     240.35
Oulu             201810     3817.52
```

### Exercise 4.2 (powers of series)

Make function `powers_of_series` that takes a Series and a positive integer `k` as parameters and returns a DataFrame. The resulting DataFrame should have the same index as the input Series. The first column of the dataFrame should be the input Series, the second column should contain the Series raised to power of two. The third column should contain the Series raised to the power of three, and so on until (and including) power of `k`. The columns should have indices from 1 to k.

The values should be numbers, but the index can have any type. Test your function from the `main` function. Example of usage:

```stylus
s = pd.Series([1,2,3,4], index=list("abcd"))
print(powers_of_series(s, 3))
```

Should print:

   1   2   3
a  1   1   1
b  2   4   8
c  3   9  27
d  4  16  64

### Exercise 4.3 (municipal information)

In the `main` function load a data set of municipal information from the `src` folder (originally from [Statistics Finland](https://pxnet2.stat.fi/PXWeb/pxweb/en/)). Use the function `pd.read_csv`, and note that the separator is a tabulator.

Print the shape of the DataFrame (number of rows and columns) and the column names in the following format:

Shape: r,c
Columns:
col1 
col2
...

Note, sometimes file ending `tsv` (tab separated values) is used instead of `csv` if the separator is a tab.

## Accessing columns and rows of a dataframe

Even though DataFrames are basically just two dimensional arrays, the way to access their elements is different from NumPy arrays. There are a couple of complications, which we will go through in this section.

Firstly, the bracket notation `[]` does not allow the use of an index pair to access a single element of the DataFrame. Instead only one dimension can be specified.

Well, does this dimension specify the rows of the DataFrame, like NumPy arrays if only one index is given, or does it specify the columns of the DataFrame?

It depends!

If an integer is used, then it specifies a column of the DataFrame in the case the **explicit** indices for the column contain that integer. In any other case an error will result. For example, with the above DataFrame, the following indexing will not work, because the explicit column index consist of the column names "Name" and "Wage" which are not integers.

```gradle
try:
    df[0]
except KeyError:
    import sys
    print("Key error", file=sys.stderr)
```

`Key error`

The following will however work.

```bash
df["Wage"]
```

0    1000
1    1500
Name: Wage, dtype: int64

As does the fancy indexing:

```lua
df[["Wage", "Name"]]
```

||Wage|Name|
|---|---|---|
|0|1000|Jack|
|1|1500|John|

If one indexes with a slice or a boolean mask, then the **rows** are referred to. Examples of these:

```apache
df[0:1]                           # slice
```

||Wage|Name|Age|
|---|---|---|---|
|0|1000|Jack|21|

```bash
df[df.Wage > 1200]               # boolean mask
```

||Wage|Name|Age|
|---|---|---|---|
|1|1500|John|29|

If some of the above calls return a Series object, then you can chain the bracket calls to get a single value from the DataFrame:

```css
df["Wage"][1]                    # Note order of dimensions
```

1500

But there is a better way to achieve this, which we will see in the next section.

### Exercise 4.4 (municipalities of finland)

Load again the municipal information DataFrame. The rows of the DataFrame correspond to various geographical areas of Finland. The first row is about Finland as a whole, then rows from Akaa to Äänekoski are municipalities of Finland in alphabetical order. After that some larger regions are listed.

Write function `municipalities_of_finland` that returns a DataFrame containing only rows about municipalities. Give an appropriate argument for `pd.read_csv` so that it interprets the column about region name as the (row) index. This way you can index the DataFrame with the names of the regions.

Test your function from the `main` function.

### Exercise 4.5 (swedish and foreigners)

Write function `swedish_and_foreigners` that

- Reads the municipalities data set
- Takes the subset about municipalities (like in previous exercise)
- Further take a subset of rows that have proportion of Swedish speaking people and proportion of foreigners both above 5 % level
- From this data set take only columns about population, the proportions of Swedish speaking people and foreigners, that is three columns.

The function should return this final DataFrame.

Do you see some kind of correlation between the columns about Swedish speaking and foreign people? Do you see correlation between the columns about the population and the proportion of Swedish speaking people in this subset?

### Exercise 4.6 (growing municipalities)

Write function `growing_municipalities` that gets subset of municipalities (a DataFrame) as a parameter and returns the proportion of municipalities with increasing population in that subset.

Test your function from the `main` function using some subset of the municipalities. Print the proportion as percentages using 1 decimal precision.

Example output:

Proportion of growing municipalities: 12.4%

## Alternative indexing and data selection

If the explanation in the previous section sounded confusing or ambiguous, or if you didn't understand a thing, you don't have to worry.

There is another way to index Pandas DataFrames, which

- allows use of index pairs to access a single element
- has the same order of dimensions as NumPy: first index specifies rows, second columns
- is not ambiguous about implicit or explicit indices

Pandas DataFrames have attributes `loc` and `iloc` that have the above qualities. You can use `loc` and `iloc` attributes and forget everything about the previous section. Or you can use these attributes and sometimes use the methods from the previous section as shortcuts if you understand them well.

The difference between `loc` and `iloc` attributes is that the former uses explicit indices and the latter uses the implicit integer indices. Examples of use:

```stylus
df.loc[1, "Wage"]
```

1500

```apache
df.iloc[-1,-1]             # Right lower corner of the DataFrame
```

29

```prolog
df.loc[1, ["Name", "Wage"]]
```

Name    John
Wage    1500
Name: 1, dtype: object

With `iloc` everything works like with NumPy arrays: indexing, slicing, fancy indexing, masking and their combinations. With `loc` it is the same but now the names in the explicit indices are used for specifying rows and columns. Make sure your understand why the above examples work as they do!

### Exercise 4.7 (subsetting with loc)

Write function `subsetting_with_loc` that in one go takes the subset of municipalities from Akaa to Äänekoski and restricts it to columns: "Population", "Share of Swedish-speakers of the population, %", and "Share of foreign citizens of the population, %". The function should return this content as a DataFrame. Use the attribute `loc`.

### Exercise 4.8 (subsetting by positions)

Write function `subsetting_by_positions` that does the following.

Read the data set of the top forty singles from the beginning of the year 1964 from the `src` folder. Return the top 10 entries and only the columns `Title` and `Artist`. Get these elements by their positions, that is, by using a single call to the `iloc` attribute. The function should return these as a DataFrame.

## Summary statistics

The summary statistic methods work in a similar way as their counter parts in NumPy. By default, the aggregation is done over columns.

```abnf
wh = pd.read_csv("https://raw.githubusercontent.com/csmastersUH/data_analysis_with_python_2020/master/kumpula-weather-2017.csv")
```

```makefile
wh2 = wh.drop(["Year", "m", "d"], axis=1)  # taking averages over these is not very interesting
wh2.mean()
```

Precipitation amount (mm)    1.966301
Snow depth (cm)              0.966480
Air temperature (degC)       6.527123
dtype: float64

The `describe` method of the `DataFrame` object gives different summary statistics for each (numeric) column. The result is a DataFrame. This method gives a good overview of the data, and is typically used in the exploratory data analysis phase.

```stata
wh.describe()
```

||Year|m|d|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|
|count|365.0|365.000000|365.000000|365.000000|358.000000|365.000000|
|mean|2017.0|6.526027|15.720548|1.966301|0.966480|6.527123|
|std|0.0|3.452584|8.808321|4.858423|3.717472|7.183934|
|min|2017.0|1.000000|1.000000|-1.000000|-1.000000|-17.800000|
|25%|2017.0|4.000000|8.000000|-1.000000|-1.000000|1.200000|
|50%|2017.0|7.000000|16.000000|0.200000|-1.000000|4.800000|
|75%|2017.0|10.000000|23.000000|2.700000|0.000000|12.900000|
|max|2017.0|12.000000|31.000000|35.000000|15.000000|19.600000|

### Exercise 4.9 (snow depth)

Write function `snow_depth` that reads in the weather DataFrame from the `src` folder and returns the maximum amount of snow in the year 2017.

Print the result in the `main` function in the following form:

Max snow depth: xx.x

### Exercise 4.10 (average temperature)

Write function `average_temperature` that reads the weather data set and returns the average temperature in July.

Print the result in the `main` function in the following form:

Average temperature in July: xx.x

### Exercise 4.11 (below zero)

Write function `below_zero` that returns the number of days when the temperature was below zero.

Print the result in the main function in the following form:

Number of days below zero: xx

## Missing data

You may have noticed something strange in the output of the `describe` method. First, the minimum value in both precipitation and snow depth fields is -1. The special value -1 means that on that day there was absolutely no snow or rain, whereas the value 0 might indicate that the value was close to zero. Secondly, the snow depth column has count 358, whereas the other columns have count 365, one measurement/value for each day of the year. How is this possible? Every field in a DataFrame should have the same number of rows. Let's use the `unique` method of the Series object to find out, which different values are used in this column:

```scss
wh["Snow depth (cm)"].unique()
```

array([ -1.,   7.,  13.,  10.,  12.,   9.,   8.,   5.,   6.,   4.,   3.,
        15.,  14.,   2.,  nan,   0.])

The `float` type allows a special value `nan` (Not A Number), in addition to normal floating point numbers. This value can represent the result from an illegal operation. For example, the operation 0/0 can either cause an exception to occur or just silently produce a `nan`. In Pandas `nan` can be used to represent a missing value. In the weather DataFrame the `nan` value tells us that the measurement from that day is not available, possibly due to a broken measuring instrument or some other problem.

Note that only float types allow the `nan` value (in Python, NumPy or Pandas). So, if we try to create an integer series with missing values, its dtype gets promoted to `float`:

```apache
pd.Series([1,3,2])
```

0    1
1    3
2    2
dtype: int64

```apache
pd.Series([1,3,2, np.nan])
```

0    1.0
1    3.0
2    2.0
3    NaN
dtype: float64

For non-numeric types the special value `None` is used to denote a missing value, and the dtype is promoted to `object`.

```mathematica
pd.Series(["jack", "joe", None])
```

0    jack
1     joe
2    None
dtype: object

Pandas excludes the missing values from the summary statistics, like we saw in the previous section. Pandas also provides some functions to handle missing values.

The missing values can be located with the `isnull` method:

```pgsql
wh.isnull()      # returns a boolean mask DataFrame
```

||Year|m|d|Time|Time zone|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|---|---|
|0|False|False|False|False|False|False|False|False|
|1|False|False|False|False|False|False|False|False|
|2|False|False|False|False|False|False|False|False|
|3|False|False|False|False|False|False|False|False|
|4|False|False|False|False|False|False|False|False|
|5|False|False|False|False|False|False|False|False|
|6|False|False|False|False|False|False|False|False|
|7|False|False|False|False|False|False|False|False|
|8|False|False|False|False|False|False|False|False|
|9|False|False|False|False|False|False|False|False|
|10|False|False|False|False|False|False|False|False|
|11|False|False|False|False|False|False|False|False|
|12|False|False|False|False|False|False|False|False|
|13|False|False|False|False|False|False|False|False|
|14|False|False|False|False|False|False|False|False|
|15|False|False|False|False|False|False|False|False|
|16|False|False|False|False|False|False|False|False|
|17|False|False|False|False|False|False|False|False|
|18|False|False|False|False|False|False|False|False|
|19|False|False|False|False|False|False|False|False|
|20|False|False|False|False|False|False|False|False|
|21|False|False|False|False|False|False|False|False|
|22|False|False|False|False|False|False|False|False|
|23|False|False|False|False|False|False|False|False|
|24|False|False|False|False|False|False|False|False|
|25|False|False|False|False|False|False|False|False|
|26|False|False|False|False|False|False|False|False|
|27|False|False|False|False|False|False|False|False|
|28|False|False|False|False|False|False|False|False|
|29|False|False|False|False|False|False|False|False|
|...|...|...|...|...|...|...|...|...|
|335|False|False|False|False|False|False|False|False|
|336|False|False|False|False|False|False|False|False|
|337|False|False|False|False|False|False|False|False|
|338|False|False|False|False|False|False|False|False|
|339|False|False|False|False|False|False|False|False|
|340|False|False|False|False|False|False|False|False|
|341|False|False|False|False|False|False|False|False|
|342|False|False|False|False|False|False|False|False|
|343|False|False|False|False|False|False|False|False|
|344|False|False|False|False|False|False|False|False|
|345|False|False|False|False|False|False|False|False|
|346|False|False|False|False|False|False|False|False|
|347|False|False|False|False|False|False|False|False|
|348|False|False|False|False|False|False|False|False|
|349|False|False|False|False|False|False|False|False|
|350|False|False|False|False|False|False|False|False|
|351|False|False|False|False|False|False|False|False|
|352|False|False|False|False|False|False|False|False|
|353|False|False|False|False|False|False|False|False|
|354|False|False|False|False|False|False|False|False|
|355|False|False|False|False|False|False|False|False|
|356|False|False|False|False|False|False|False|False|
|357|False|False|False|False|False|False|False|False|
|358|False|False|False|False|False|False|False|False|
|359|False|False|False|False|False|False|False|False|
|360|False|False|False|False|False|False|False|False|
|361|False|False|False|False|False|False|False|False|
|362|False|False|False|False|False|False|False|False|
|363|False|False|False|False|False|False|False|False|
|364|False|False|False|False|False|False|False|False|

365 rows × 8 columns

This is not very useful as we cannot directly use the mask to index the DataFrame. We can, however, combine it with the `any` method to find out all the rows that contain at least one missing value:

```jboss-cli
wh[wh.isnull().any(axis=1)]
```

||Year|m|d|Time|Time zone|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|---|---|
|74|2017|3|16|00:00|UTC|1.8|NaN|3.4|
|163|2017|6|13|00:00|UTC|0.6|NaN|12.6|
|308|2017|11|5|00:00|UTC|0.2|NaN|8.4|
|309|2017|11|6|00:00|UTC|2.0|NaN|7.5|
|313|2017|11|10|00:00|UTC|3.6|NaN|7.2|
|321|2017|11|18|00:00|UTC|11.3|NaN|5.9|
|328|2017|11|25|00:00|UTC|8.5|NaN|4.2|

The `notnull` method works conversively to the `isnull` method.

The `dropna` method of a DataFrame drops columns or rows that contain missing values from the DataFrame, depending on the `axis` parameter.

```jboss-cli
wh.dropna().shape   # Default axis is 0
```

(358, 8)

```jboss-cli
wh.dropna(axis=1).shape # Drops the columns containing missing values
```

(365, 7)

The `how` and `thresh` parameters of the `dropna` method allow one to specify how many values need to be missing in order for the row/column to be dropped.

The `fillna` method allows to fill the missing values with some constant or interpolated values. The `method` parameter can be:

- `None`: use the given positional parameter as the constant to fill missing values with
- `ffill`: use the previous value to fill the current value
- `bfill`: use the next value to fill the current value

For example, for the weather data we could use forward fill

```oxygene
wh = wh.fillna(method='ffill')
wh[wh.isnull().any(axis=1)]
```

||Year|m|d|Time|Time zone|Precipitation amount (mm)|Snow depth (cm)|Air temperature (degC)|
|---|---|---|---|---|---|---|---|---|

The `interpolate` method, which we will not cover here, offers more elaborate ways to interpolate the missing values from their neighbouring non-missing values.

### Exercise 4.12 (cyclists)

Write function `cyclists` that does the following.

Load the Helsinki bicycle data set from the `src` folder ([https://hri.fi/data/dataset/helsingin-pyorailijamaarat](https://hri.fi/data/dataset/helsingin-pyorailijamaarat)). The dataset contains the number of cyclists passing by measuring points per hour. The data is gathered over about four years, and there are 20 measuring points around Helsinki. The dataset contains some empty rows at the end. Get rid of these. Also, get rid of columns that contain only missing values. Return the cleaned dataset.

### Exercise 4.13 (missing value types)

Make function `missing_value_types` that returns the following DataFrame. Use the `State` column as the (row) index. The value types for the two other columns should be `float` and `object`, respectively. Replace the dashes with the appropriate missing value symbols.

|State|Year of independence|President|
|---|---|---|
|United Kingdom|-|-|
|Finland|1917|Niinistö|
|USA|1776|Trump|
|Sweden|1523|-|
|Germany|-|Steinmeier|
|Russia|1992|Putin|

### Exercise 4.14 (special missing values)

Write function `special_missing_values` that does the following.

Read the data set of the top forty singles from the beginning of the year 1964 from the `src` folder. Return the rows whose singles' position dropped compared to last week's position (column LW=Last Week).

To do this you first have to convert the special values "New" and "Re" (Re-entry) to missing values (`None`).

### Exercise 4.15 (last week)

This exercise can give two points at maximum!

Write function `last_week` that reads the top40 data set mentioned in the above exercise. The function should then try to reconstruct the top40 list of the previous week based on that week's list. Try to do this as well as possible. You can fill the values that are impossible to reconstruct by missing value symbols. Your solution should work for a top40 list of any week. So don't rely on specific features of this top40 list. The column `WoC` means "Weeks on Chart", that is, on how many weeks this song has been on the top 40 list.

Hint. First create the last week's top40 list of those songs that are also on this week's list. Then add those entries that were not on this week's list. Finally sort by position.

Hint 2. The `where` method of Series and DataFrame can be useful. It can also be nested.

Hint 3. Like in NumPy, you can use with Pandas the bitwise operators `&`, `|`, and `~`. Remember that the bitwise operators have higher precedence than the comparison operations, so you may have to use parentheses around comparisons, if you combined result of comparisons with bitwise operators.

You get a second point, if you get the columns `LW` and `Peak Pos` correct.

## Converting columns from one type to another

There are several ways of converting a column to another type. For converting single columns (a Series) one can use the `pd.to_numeric` function or the `map` method. For converting several columns in one go one can use the `astype` method. We will give a few examples of use of these methods/functions. For more details, look from the Pandas documentation.

```go
pd.Series(["1","2"]).map(int)                           # str -> int
```

0    1
1    2
dtype: int64

```processing
pd.Series([1,2]).map(str)                               # int -> str
```

0    1
1    2
dtype: object

```apache
pd.to_numeric(pd.Series([1,1.0]), downcast="integer")   # object -> int
```

0    1
1    1
dtype: int8

```pgsql
pd.to_numeric(pd.Series([1,"a"]), errors="coerce")      # conversion error produces Nan
```

0    1.0
1    NaN
dtype: float64

```elm
pd.Series([1,2]).astype(str)                            # works for a single series
```

0    1
1    2
dtype: object

```stylus
df = pd.DataFrame({"a": [1,2,3], "b" : [4,5,6], "c" : [7,8,9]})
print(df.dtypes)
print(df)
```

`a int64   b int64   c int64   dtype: object   a b c   0 1 4 7   1 2 5 8   2 3 6 9`

```elm
df.astype(float)                       # Convert all columns
```

||a|b|c|
|---|---|---|---|
|0|1.0|4.0|7.0|
|1|2.0|5.0|8.0|
|2|3.0|6.0|9.0|

```stylus
df2 = df.astype({"b" : float, "c" : str})    # different types for columns
print(df2.dtypes)
print(df2)
```

`a int64   b float64   c object   dtype: object   a b c   0 1 4.0 7   1 2 5.0 8   2 3 6.0 9`

## String processing

If the elements in a column are strings, then the vectorized versions of Python's string processing methods are available. These are accessed through the `str` attribute of a Series or a DataFrame. For example, to capitalize all the strings of a Series, we can use the `str.capitalize` method:

```stylus
names = pd.Series(["donald", "theresa", "angela", "vladimir"])
names.str.capitalize()
```

0      Donald
1     Theresa
2      Angela
3    Vladimir
dtype: object

One can find all the available methods by pressing the tab key after the text `names.str.` in a Python prompt. Try it in below cell!

```stylus
#names.str.
```

We can split a column or Series into several columns using the `split` method. For example:

```stylus
full_names = pd.Series(["Donald Trump", "Theresa May", "Angela Merkel", "Vladimir Putin"])
full_names.str.split()
```

0      [Donald, Trump]
1       [Theresa, May]
2     [Angela, Merkel]
3    [Vladimir, Putin]
dtype: object

This is not exactly what we wanted: now each element is a list. We need to use the `expand` parameter to split into columns:

```routeros
full_names.str.split(expand=True)
```

||0|1|
|---|---|---|
|0|Donald|Trump|
|1|Theresa|May|
|2|Angela|Merkel|
|3|Vladimir|Putin|

### Exercise 4.16 (split date)

Read again the bicycle data set from `src` folder, and clean it as in the earlier exercise. Then split the `Päivämäärä` column into a DataFrame with five columns with column names `Weekday`, `Day`, `Month`, `Year`, and `Hour`. Note that you also need to to do some conversions. To get Hours, drop the colon and minutes. Convert field `Weekday` according the following rule:

ma -> Mon
ti -> Tue
ke -> Wed
to -> Thu
pe -> Fri
la -> Sat
su -> Sun

Convert the `Month` column according to the following mapping

tammi 1
helmi 2
maalis 3
huhti 4
touko 5
kesä 6
heinä 7
elo 8
syys 9
loka 10
marras 11
joulu 12

Create function `split_date` that does the above and returns a DataFrame with five columns. You may want to use the `map` method of Series objects.

So the first element in the `Päivämäärä` column of the original data set should be converted from `ke 1 tammi 2014 00:00` to `Wed 1 1 2014 0` . Test your solution from the `main` function.

### Exercise 4.17 (cleaning data)

This exercise can give two points at maximum!

The entries in the following table of US presidents are not uniformly formatted. Make function `cleaning_data` that reads the table from the tsv file `src/presidents.tsv` and returns the cleaned version of it. Note, you must do the edits programmatically using the string edit methods, not by creating a new DataFrame by hand. The columns should have `dtype`s `object`, `integer`, `float`, `integer`, `object`. The `where` method of DataFrames can be helpful, likewise the [string methods](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html#string-methods) of Series objects. You get an additional point, if you manage to get the columns President and Vice-president right!

|President|Start|Last|Seasons|Vice-president|
|---|---|---|---|---|
|donald trump|2017 Jan|-|1|Mike pence|
|barack obama|2009|2017|2|joe Biden|
|bush, george|2001|2009|2|Cheney, dick|
|Clinton, Bill|1993|2001|two|gore, Al|

## Additional information

We covered subsetting of DataFrames with the indexers `[]`, `.loc[]`, and `.iloc[]` quite concisely. For a more verbose explanation, look at the [tutorials at Dunder Data](https://medium.com/dunder-data/pandas-tutorials/home). Especially, the problems with chained indexing operators (like `df["a"][1]`) are explained well there (tutorial 4), which we did not cover at all. As a rule of thumb: one should avoid chained indexing combined with assignment! See [Pandas documentation](http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#why-does-assignment-fail-when-using-chained-indexing).

## Summary (week 4)

- You can create DataFrames in several ways:
    
    - By reading from a csv file
    - Out out two dimensional NumPy array
    - Out of rows
    - Out of columns
    
- You know how to access rows, columns and individual elements of DataFrames
- You can use the `describe` method to get a quick overview of a DataFrame
- You know how missing values are represented in Series and DataFrames, and you know how to manipulate them
- There are similarities between Python's string methods and the vectorized forms of string operations in Series and DataFrames
- You can do complicated text processing with the `str.replace` method combined with regular expressions
- The powerful `where` method is the vectorized form of Python's `if-else` construct
- We remember that with NumPy arrays we preferred vectorized operations instead of, for instance, `for` loops. Same goes with Pandas. It may first feel that things are easier to achieve with loops, but after a while vectorized operations will feel natural.


```elm
import pandas as pd
import numpy as np
```

## Catenating datasets

We already saw in the NumPy section how we can catenate arrays along an axis: `axis=0`catenates vertically and `axis=1` catenates horizontally, and so on. With the DataFrames of Pandas it works similarly except that the row indices and the column names require extra attention. Also note a slight difference in the name: `np.concatenate` but `pd.concat`.

Let's start by considering catenation along the axis 0, that is, vertical catenation. We will first make a helper function to easily create DataFrames for testing.

```haskell
def makedf(cols, ind):
    data = {c : [str(c) + str(i) for i in ind] for c in cols}
    return pd.DataFrame(data, ind)
```

Next we will create some example DataFrames:

```livecodeserver
a=makedf("AB", [0,1])
a
```

||A|B|
|---|---|---|
|0|A0|B0|
|1|A1|B1|

```stylus
b=makedf("AB", [2,3])
b
```

||A|B|
|---|---|---|
|2|A2|B2|
|3|A3|B3|

```llvm
c=makedf("CD", [0,1])
c
```

||C|D|
|---|---|---|
|0|C0|D0|
|1|C1|D1|

```stylus
d=makedf("BC", [2,3])
d
```

||B|C|
|---|---|---|
|2|B2|C2|
|3|B3|C3|

In the following simple case, the `concat` function works exactly as we expect it would:

```livecodeserver
pd.concat([a,b])   # The default axis is 0
```

||A|B|
|---|---|---|
|0|A0|B0|
|1|A1|B1|
|2|A2|B2|
|3|A3|B3|

The next, however, will create duplicate indices:

```livecodeserver
r=pd.concat([a,a])
r
```

||A|B|
|---|---|---|
|0|A0|B0|
|1|A1|B1|
|0|A0|B0|
|1|A1|B1|

```stylus
r.loc[0,"A"]
```

0    A0
0    A0
Name: A, dtype: object

This is not usually what we want! There are three solutions to this. Firstly, deny creation of duplicated indices by giving the `verify_integrity` parameter to the `concat` function:

```routeros
try:
    pd.concat([a,a], verify_integrity=True)
except ValueError as e:
    import sys
    print(e, file=sys.stderr)
```

`Indexes have overlapping values: Int64Index([0, 1], dtype='int64')`

Secondly, we can ask for automatic renumbering of rows:

```routeros
pd.concat([a,a], ignore_index=True)
```

||A|B|
|---|---|---|
|0|A0|B0|
|1|A1|B1|
|2|A0|B0|
|3|A1|B1|

Thirdly, we can ask for _hierarchical indexing_. The indices can contain multiple levels, but on this course we don't consider hierarchical indices in detail. Hierarchical indices can make a two dimensional array to work like higher dimensional array.

```livecodeserver
r2=pd.concat([a,a], keys=['first', 'second'])
r2
```

|||A|B|
|---|---|---|---|
|first|0|A0|B0|
||1|A1|B1|
|second|0|A0|B0|
||1|A1|B1|

```css
r2["A"]["first"][0]
```

'A0'

Everything works similarly, when we want to catenate horizontally:

```routeros
pd.concat([a,c], axis=1)
```

||A|B|C|D|
|---|---|---|---|---|
|0|A0|B0|C0|D0|
|1|A1|B1|C1|D1|

We have so far assumed that when concatenating vertically the columns of both DataFrames are the same, and when joining horizontally the indices are the same. This is, however, not required:

```livecodeserver
pd.concat([a,d], sort=False)    # sort option is used to silence a deprecation message
```

||A|B|C|
|---|---|---|---|
|0|A0|B0|NaN|
|1|A1|B1|NaN|
|2|NaN|B2|C2|
|3|NaN|B3|C3|

It expanded the non-existing cases with `NaN`s. This method is called an _outer join_, which forms the union of columns in the two DataFrames. The alternative is _inner join_, which forms the intersection of columns:

```maxima
pd.concat([a,d], join="inner")
```

||B|
|---|---|
|0|B0|
|1|B1|
|2|B2|
|3|B3|

### Exercise 5.1 (split date continues)

Write function `split_date_continues` that does

- read the bicycle data set
- clean the data set of columns/rows that contain only missing values
- drops the `Päivämäärä` column and replaces it with its splitted components as before

Use the `concat` function to do this. The function should return a DataFrame with 25 columns (first five related to the date and then the rest 20 concerning the measument location.

**Hint**: You may use your solution or the model solution from exercise 16 of the previous set as a starting point.

## Merging dataframes

Merging combines two DataFrames based on some common field.

Let's recall the earlier DataFrame about wages and ages of persons:

```prolog
df = pd.DataFrame([[1000, "Jack", 21], [1500, "John", 29]], columns=["Wage", "Name", "Age"])
df
```

||Wage|Name|Age|
|---|---|---|---|
|0|1000|Jack|21|
|1|1500|John|29|

Now, create a new DataFrame with the occupations of persons:

```stylus
df2 = pd.DataFrame({"Name" : ["John", "Jack"], "Occupation": ["Plumber", "Carpenter"]})
df2
```

||Name|Occupation|
|---|---|---|
|0|John|Plumber|
|1|Jack|Carpenter|

The following function call will merge the two DataFrames on their common field, and, importantly, will keep the indices _aligned_. What this means is that even though the names are listed in different order in the two frames, the merge will still give correct result.

```bash
pd.merge(df, df2)
```

||Wage|Name|Age|Occupation|
|---|---|---|---|---|
|0|1000|Jack|21|Carpenter|
|1|1500|John|29|Plumber|

This was an example of a simple one-to-one merge, where the keys in the `Name` columns had 1-to-1 correspondence. Sometimes not all the keys appear in both DataFrames:

```prolog
df3 = pd.concat([df2, pd.DataFrame({ "Name" : ["James"], "Occupation":["Painter"]})], ignore_index=True)
df3
```

||Name|Occupation|
|---|---|---|
|0|John|Plumber|
|1|Jack|Carpenter|
|2|James|Painter|

```pgsql
pd.merge(df, df3)                # By default an inner join is computed
```

||Wage|Name|Age|Occupation|
|---|---|---|---|---|
|0|1000|Jack|21|Carpenter|
|1|1500|John|29|Plumber|

```bash
pd.merge(df, df3, how="outer")   # Outer join
```

||Wage|Name|Age|Occupation|
|---|---|---|---|---|
|0|1000.0|Jack|21.0|Carpenter|
|1|1500.0|John|29.0|Plumber|
|2|NaN|James|NaN|Painter|

Also, many-to-one and many-to-many relationships can occur in merges:

```stylus
books = pd.DataFrame({"Title" : ["War and Peace", "Good Omens", "Good Omens"] , 
                      "Author" : ["Tolstoi", "Terry Pratchett", "Neil Gaiman"]})
books
```

||Title|Author|
|---|---|---|
|0|War and Peace|Tolstoi|
|1|Good Omens|Terry Pratchett|
|2|Good Omens|Neil Gaiman|

```prolog
collections = pd.DataFrame([["Oodi", "War and Peace"],
                           ["Oodi", "Good Omens"],
                           ["Pasila", "Good Omens"],
                           ["Kallio", "War and Peace"]], columns=["Library", "Title"])
collections
```

||Library|Title|
|---|---|---|
|0|Oodi|War and Peace|
|1|Oodi|Good Omens|
|2|Pasila|Good Omens|
|3|Kallio|War and Peace|

All combinations with matching keys (`Title`) are created:

```ceylon
libraries_with_books_by = pd.merge(books, collections)
libraries_with_books_by
```

||Title|Author|Library|
|---|---|---|---|
|0|War and Peace|Tolstoi|Oodi|
|1|War and Peace|Tolstoi|Kallio|
|2|Good Omens|Terry Pratchett|Oodi|
|3|Good Omens|Terry Pratchett|Pasila|
|4|Good Omens|Neil Gaiman|Oodi|
|5|Good Omens|Neil Gaiman|Pasila|

### Exercise 5.2 (cycling weather)

Merge the processed cycling data set (from the previous exercise) and weather data set along the columns year, month, and day. Note that the names of these columns might be different in the two tables: use the `left_on` and `right_on` parameters. Then drop useless columns 'm', 'd', 'Time', and 'Time zone'.

Write function `cycling_weather` that reads the data sets and returns the resulting DataFrame.

### Exercise 5.3 (top bands)

Merge the DataFrames UK top40 and the bands DataFrame that are stored in the `src` folder. Do all this in the parameterless function `top_bands`, which should return the merged DataFrame. Use the `left_on` and `right_on` parameters to `merge`. Test your function from the `main` function.

## Aggregates and groupings

Let us use again the weather dataset. First, we make the column names a bit more uniform and concise. For example the columns `Year`, `m`, and `d` are not uniformly named.

We can easily change the column names with the `rename` method of the DataFrame. Note that we cannot directly change the index `wh.columns` as it is immutable.

```abnf
wh = pd.read_csv("https://raw.githubusercontent.com/csmastersUH/data_analysis_with_python_2020/master/kumpula-weather-2017.csv")
```

```stylus
wh3 = wh.rename(columns={"m": "Month", "d": "Day", "Precipitation amount (mm)" : "Precipitation", 
                         "Snow depth (cm)" : "Snow", "Air temperature (degC)" : "Temperature"})
wh3.head()
```

||Year|Month|Day|Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|UTC|-1.0|-1.0|0.6|
|1|2017|1|2|00:00|UTC|4.4|-1.0|-3.9|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|
|3|2017|1|4|00:00|UTC|-1.0|13.0|-12.8|
|4|2017|1|5|00:00|UTC|-1.0|10.0|-17.8|

Pandas has an operation that splits a DataFrame into groups, performs some operation on each of the groups, and then combines the result from each group into a resulting DataFrame. This split-apply-combine functionality is really flexible and powerful operation. In Pandas you start by calling the `groupby` method, which splits the DataFrame into groups. In the following example the rows that contain measurements from the same month belong to the same group:

```abnf
groups = wh3.groupby("Month")
groups
```

<pandas.core.groupby.generic.DataFrameGroupBy object at 0x7fa1a21d32b0>

Nothing happened yet, but the `groupby` object knows how the division into groups is done. This is called a lazy operation. We can query the number of groups in the `groupby` object:

```stylus
len(groups)
```

12

We can iterate through all the groups:

```sas
for key, group in groups:
    print(key, len(group))
```

`1 31   2 28   3 31   4 30   5 31   6 30   7 31   8 31   9 30   10 31   11 30   12 31`

```pgsql
groups.get_group(2)                 # Group with index two is February
```

||Year|Month|Day|Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|---|---|---|
|31|2017|2|1|00:00|UTC|1.5|4.0|-0.6|
|32|2017|2|2|00:00|UTC|0.2|5.0|-0.8|
|33|2017|2|3|00:00|UTC|-1.0|6.0|-0.2|
|34|2017|2|4|00:00|UTC|2.7|6.0|0.4|
|35|2017|2|5|00:00|UTC|-1.0|7.0|-2.5|
|36|2017|2|6|00:00|UTC|-1.0|7.0|-7.3|
|37|2017|2|7|00:00|UTC|-1.0|8.0|-12.1|
|38|2017|2|8|00:00|UTC|-1.0|8.0|-8.8|
|39|2017|2|9|00:00|UTC|-1.0|8.0|-10.1|
|40|2017|2|10|00:00|UTC|-1.0|8.0|-8.3|
|41|2017|2|11|00:00|UTC|-1.0|8.0|-5.4|
|42|2017|2|12|00:00|UTC|-1.0|8.0|-2.7|
|43|2017|2|13|00:00|UTC|-1.0|8.0|1.5|
|44|2017|2|14|00:00|UTC|-1.0|8.0|4.4|
|45|2017|2|15|00:00|UTC|-1.0|8.0|0.0|
|46|2017|2|16|00:00|UTC|0.9|8.0|0.5|
|47|2017|2|17|00:00|UTC|0.2|8.0|1.5|
|48|2017|2|18|00:00|UTC|1.5|5.0|1.9|
|49|2017|2|19|00:00|UTC|1.1|5.0|2.2|
|50|2017|2|20|00:00|UTC|2.8|3.0|0.4|
|51|2017|2|21|00:00|UTC|-1.0|7.0|-2.5|
|52|2017|2|22|00:00|UTC|12.2|6.0|-4.6|
|53|2017|2|23|00:00|UTC|0.3|15.0|-0.7|
|54|2017|2|24|00:00|UTC|-1.0|13.0|-5.3|
|55|2017|2|25|00:00|UTC|0.4|13.0|-5.6|
|56|2017|2|26|00:00|UTC|2.5|12.0|-2.0|
|57|2017|2|27|00:00|UTC|1.0|14.0|-2.3|
|58|2017|2|28|00:00|UTC|7.7|13.0|2.1|

The `groupby` object functions a bit like a DataFrame, so some operations which are allowed for DataFrames are also allowed for the `groupby` object. For example, we can get a subset of columns:

```bash
groups["Temperature"]
```

<pandas.core.groupby.generic.SeriesGroupBy object at 0x7fa15af92be0>

For each DataFrame corresponding to a group the Temperature column was chosen. Still nothing was shown, because we haven't applied any operation on the groups.

The common methods also include the aggregation methods. Let's try to apply the `mean`aggregation:

```scss
groups["Temperature"].mean()
```

```apache
Month
1     -2.316129
2     -2.389286
3      0.983871
4      2.676667
5      9.783871
6     13.726667
7     16.035484
8     16.183871
9     11.826667
10     5.454839
11     3.950000
12     1.741935
Name: Temperature, dtype: float64
```

Now what happened was that after the mean aggregation was performed on each group, the results were automatically combined into a resulting DataFrame. Let's try some other aggregation:

```bash
groups["Precipitation"].sum()
```

```apache
Month
1      26.9
2      21.0
3      29.7
4      26.9
5      -5.9
6      59.3
7      14.2
8      70.1
9      51.2
10    173.5
11    117.2
12    133.6
Name: Precipitation, dtype: float64
```

Ok, the -1.0 values in the Precipitation field are causing trouble here, let's convert them to zeros:

```stylus
wh4 = wh3.copy()
wh4.loc[wh4.Precipitation == -1, "Precipitation"] = 0
wh4.loc[wh4.Snow == -1, "Snow"] = 0
wh4.head()
```

||Year|Month|Day|Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|UTC|0.0|0.0|0.6|
|1|2017|1|2|00:00|UTC|4.4|0.0|-3.9|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|
|3|2017|1|4|00:00|UTC|0.0|13.0|-12.8|
|4|2017|1|5|00:00|UTC|0.0|10.0|-17.8|

```stylus
wh4.groupby("Month")["Precipitation"].sum()
```

```apache
Month
1      38.9
2      35.0
3      41.7
4      39.9
5      16.1
6      76.3
7      31.2
8      86.1
9      65.2
10    184.5
11    120.2
12    140.6
Name: Precipitation, dtype: float64
```

### Other ways to operate on groups

The aggregations are not the only possible operations on groups. The other possibilities are filtering, transformation, and application.

In **filtering** some of the groups can be filtered out.

```python
def myfilter(df):                                     # The filter function must return a boolean value
    return df["Precipitation"].sum() >= 150

wh4.groupby("Month").filter(myfilter)                 # Filter out months with total precipitation less that 150 mm
```

||Year|Month|Day|Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|---|---|---|
|273|2017|10|1|00:00|UTC|0.0|0.0|9.1|
|274|2017|10|2|00:00|UTC|6.4|0.0|9.2|
|275|2017|10|3|00:00|UTC|21.5|0.0|8.3|
|276|2017|10|4|00:00|UTC|12.7|0.0|11.2|
|277|2017|10|5|00:00|UTC|0.6|0.0|8.8|
|278|2017|10|6|00:00|UTC|0.7|0.0|7.7|
|279|2017|10|7|00:00|UTC|11.7|0.0|8.1|
|280|2017|10|8|00:00|UTC|14.1|0.0|9.3|
|281|2017|10|9|00:00|UTC|18.3|0.0|8.6|
|282|2017|10|10|00:00|UTC|24.2|0.0|8.1|
|283|2017|10|11|00:00|UTC|1.5|0.0|6.9|
|284|2017|10|12|00:00|UTC|18.1|0.0|6.0|
|285|2017|10|13|00:00|UTC|0.0|0.0|7.5|
|286|2017|10|14|00:00|UTC|5.0|0.0|7.2|
|287|2017|10|15|00:00|UTC|3.3|0.0|8.3|
|288|2017|10|16|00:00|UTC|0.0|0.0|10.7|
|289|2017|10|17|00:00|UTC|1.6|0.0|8.5|
|290|2017|10|18|00:00|UTC|0.0|0.0|8.3|
|291|2017|10|19|00:00|UTC|0.9|0.0|4.6|
|292|2017|10|20|00:00|UTC|0.0|0.0|2.0|
|293|2017|10|21|00:00|UTC|0.0|0.0|0.2|
|294|2017|10|22|00:00|UTC|0.0|0.0|0.1|
|295|2017|10|23|00:00|UTC|0.0|0.0|1.3|
|296|2017|10|24|00:00|UTC|0.0|0.0|0.8|
|297|2017|10|25|00:00|UTC|8.5|0.0|2.1|
|298|2017|10|26|00:00|UTC|12.3|2.0|0.3|
|299|2017|10|27|00:00|UTC|2.7|7.0|-0.3|
|300|2017|10|28|00:00|UTC|17.1|4.0|3.3|
|301|2017|10|29|00:00|UTC|3.3|0.0|2.1|
|302|2017|10|30|00:00|UTC|0.0|0.0|1.2|
|303|2017|10|31|00:00|UTC|0.0|0.0|-0.4|

In a **transformation** each group's DataFrame is manipulated in a way that retains its shape. An example of centering values, so that the deviations from the monthly means are shown:

```stylus
pd.concat([wh4.iloc[:, 0:3], 
           wh4.groupby("Month")[["Precipitation", "Snow", "Temperature"]].transform(lambda x : x - x.mean())], 
          axis=1)
```

||Year|Month|Day|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|---|
|0|2017|1|1|-1.254839|-6.903226|2.916129|
|1|2017|1|2|3.145161|-6.903226|-1.583871|
|2|2017|1|3|5.345161|0.096774|-4.183871|
|3|2017|1|4|-1.254839|6.096774|-10.483871|
|4|2017|1|5|-1.254839|3.096774|-15.483871|
|5|2017|1|6|-0.954839|3.096774|-15.483871|
|6|2017|1|7|4.045161|3.096774|-1.483871|
|7|2017|1|8|-1.254839|5.096774|1.816129|
|8|2017|1|9|-0.154839|5.096774|2.816129|
|9|2017|1|10|-0.954839|2.096774|4.016129|
|10|2017|1|11|-1.254839|0.096774|0.716129|
|11|2017|1|12|6.745161|0.096774|-0.483871|
|12|2017|1|13|-1.154839|6.096774|3.416129|
|13|2017|1|14|-1.154839|1.096774|3.116129|
|14|2017|1|15|-1.254839|1.096774|-0.483871|
|15|2017|1|16|-1.254839|1.096774|-1.883871|
|16|2017|1|17|-1.054839|1.096774|-1.183871|
|17|2017|1|18|-0.354839|1.096774|3.416129|
|18|2017|1|19|-1.254839|-1.903226|3.916129|
|19|2017|1|20|-0.954839|-1.903226|1.716129|
|20|2017|1|21|-0.854839|-1.903226|0.516129|
|21|2017|1|22|-1.054839|-1.903226|3.316129|
|22|2017|1|23|-1.154839|-0.903226|2.416129|
|23|2017|1|24|-1.254839|-0.903226|0.116129|
|24|2017|1|25|-0.654839|-0.903226|-1.483871|
|25|2017|1|26|-1.254839|-0.903226|4.216129|
|26|2017|1|27|-1.254839|-2.903226|3.916129|
|27|2017|1|28|0.545161|-2.903226|3.116129|
|28|2017|1|29|1.345161|-3.903226|2.916129|
|29|2017|1|30|4.345161|-1.903226|3.316129|
|...|...|...|...|...|...|...|
|335|2017|12|2|0.764516|3.516129|-0.341935|
|336|2017|12|3|2.664516|-1.483871|3.258065|
|337|2017|12|4|-4.535484|-1.483871|-0.441935|
|338|2017|12|5|-3.835484|-1.483871|-1.741935|
|339|2017|12|6|-4.535484|-1.483871|-2.941935|
|340|2017|12|7|11.764516|-1.483871|-2.541935|
|341|2017|12|8|-2.535484|-1.483871|3.458065|
|342|2017|12|9|-4.335484|-1.483871|2.458065|
|343|2017|12|10|-4.535484|-1.483871|0.258065|
|344|2017|12|11|-3.235484|-1.483871|-0.341935|
|345|2017|12|12|30.464516|-1.483871|-0.141935|
|346|2017|12|13|-0.335484|3.516129|-0.141935|
|347|2017|12|14|0.664516|2.516129|-0.141935|
|348|2017|12|15|5.464516|8.516129|-0.041935|
|349|2017|12|16|-3.235484|4.516129|0.658065|
|350|2017|12|17|-4.535484|3.516129|-1.641935|
|351|2017|12|18|-1.035484|3.516129|0.258065|
|352|2017|12|19|-4.335484|1.516129|-0.741935|
|353|2017|12|20|-0.935484|1.516129|0.858065|
|354|2017|12|21|-4.535484|-1.483871|0.758065|
|355|2017|12|22|-4.535484|-1.483871|-1.841935|
|356|2017|12|23|3.064516|-1.483871|-0.541935|
|357|2017|12|24|-4.535484|-1.483871|-2.041935|
|358|2017|12|25|1.364516|-1.483871|-1.441935|
|359|2017|12|26|3.264516|-1.483871|0.158065|
|360|2017|12|27|-3.435484|-1.483871|2.058065|
|361|2017|12|28|-0.835484|-1.483871|1.058065|
|362|2017|12|29|3.264516|-1.483871|2.058065|
|363|2017|12|30|-0.435484|-1.483871|0.758065|
|364|2017|12|31|-1.335484|-1.483871|-0.141935|

365 rows × 6 columns

The **apply** method is very generic and only requires that for each group's DataFrame the given function returns a DataFrame, Series, or a scalar. In the following example, we sort within each group by the temperature:

```stylus
wh4.groupby("Month").apply(lambda df : df.sort_values("Temperature"))
```

|||Year|Month|Day|Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|---|---|---|---|
|Month||||||||||
|---|---|---|---|---|---|---|---|---|---|
|1|4|2017|1|5|00:00|UTC|0.0|10.0|-17.8|
|5|2017|1|6|00:00|UTC|0.3|10.0|-17.8|
|3|2017|1|4|00:00|UTC|0.0|13.0|-12.8|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|
|15|2017|1|16|00:00|UTC|0.0|8.0|-4.2|
|1|2017|1|2|00:00|UTC|4.4|0.0|-3.9|
|24|2017|1|25|00:00|UTC|0.6|6.0|-3.8|
|6|2017|1|7|00:00|UTC|5.3|10.0|-3.8|
|16|2017|1|17|00:00|UTC|0.2|8.0|-3.5|
|11|2017|1|12|00:00|UTC|8.0|7.0|-2.8|
|14|2017|1|15|00:00|UTC|0.0|8.0|-2.8|
|23|2017|1|24|00:00|UTC|0.0|6.0|-2.2|
|20|2017|1|21|00:00|UTC|0.4|5.0|-1.8|
|10|2017|1|11|00:00|UTC|0.0|7.0|-1.6|
|19|2017|1|20|00:00|UTC|0.3|5.0|-0.6|
|7|2017|1|8|00:00|UTC|0.0|12.0|-0.5|
|22|2017|1|23|00:00|UTC|0.1|6.0|0.1|
|30|2017|1|31|00:00|UTC|0.0|4.0|0.2|
|8|2017|1|9|00:00|UTC|1.1|12.0|0.5|
|28|2017|1|29|00:00|UTC|2.6|3.0|0.6|
|0|2017|1|1|00:00|UTC|0.0|0.0|0.6|
|13|2017|1|14|00:00|UTC|0.1|8.0|0.8|
|27|2017|1|28|00:00|UTC|1.8|4.0|0.8|
|29|2017|1|30|00:00|UTC|5.6|5.0|1.0|
|21|2017|1|22|00:00|UTC|0.2|5.0|1.0|
|12|2017|1|13|00:00|UTC|0.1|13.0|1.1|
|17|2017|1|18|00:00|UTC|0.9|8.0|1.1|
|18|2017|1|19|00:00|UTC|0.0|5.0|1.6|
|26|2017|1|27|00:00|UTC|0.0|4.0|1.6|
|9|2017|1|10|00:00|UTC|0.3|9.0|1.7|
|...|...|...|...|...|...|...|...|...|...|
|12|340|2017|12|7|00:00|UTC|16.3|0.0|-0.8|
|357|2017|12|24|00:00|UTC|0.0|0.0|-0.3|
|355|2017|12|22|00:00|UTC|0.0|0.0|-0.1|
|338|2017|12|5|00:00|UTC|0.7|0.0|0.0|
|350|2017|12|17|00:00|UTC|0.0|5.0|0.1|
|358|2017|12|25|00:00|UTC|5.9|0.0|0.3|
|334|2017|12|1|00:00|UTC|3.4|0.0|0.9|
|352|2017|12|19|00:00|UTC|0.2|3.0|1.0|
|356|2017|12|23|00:00|UTC|7.6|0.0|1.2|
|337|2017|12|4|00:00|UTC|0.0|0.0|1.3|
|335|2017|12|2|00:00|UTC|5.3|5.0|1.4|
|344|2017|12|11|00:00|UTC|1.3|0.0|1.4|
|364|2017|12|31|00:00|UTC|3.2|0.0|1.6|
|346|2017|12|13|00:00|UTC|4.2|5.0|1.6|
|345|2017|12|12|00:00|UTC|35.0|0.0|1.6|
|347|2017|12|14|00:00|UTC|5.2|4.0|1.6|
|348|2017|12|15|00:00|UTC|10.0|10.0|1.7|
|359|2017|12|26|00:00|UTC|7.8|0.0|1.9|
|351|2017|12|18|00:00|UTC|3.5|5.0|2.0|
|343|2017|12|10|00:00|UTC|0.0|0.0|2.0|
|349|2017|12|16|00:00|UTC|1.3|6.0|2.4|
|363|2017|12|30|00:00|UTC|4.1|0.0|2.5|
|354|2017|12|21|00:00|UTC|0.0|0.0|2.5|
|353|2017|12|20|00:00|UTC|3.6|3.0|2.6|
|361|2017|12|28|00:00|UTC|3.7|0.0|2.8|
|360|2017|12|27|00:00|UTC|1.1|0.0|3.8|
|362|2017|12|29|00:00|UTC|7.8|0.0|3.8|
|342|2017|12|9|00:00|UTC|0.2|0.0|4.2|
|336|2017|12|3|00:00|UTC|7.2|0.0|5.0|
|341|2017|12|8|00:00|UTC|2.0|0.0|5.2|

365 rows × 8 columns

### Exercise 5.4 (cyclists per day)

This exercise can give two points at maximum!

Part 1.

Read, clean and parse the bicycle data set as before. Group the rows by year, month, and day. Get the sum for each group. Make function `cyclists_per_day` that does the above. The function should return a DataFrame. Make sure that the columns Hour and Weekday are not included in the returned DataFrame.

Part 2.

In the `main` function, using the function `cyclists_per_day`, get the daily counts. The index of the DataFrame now consists of tuples (Year, Month, Day). Then restrict this data to August of year 2017, and plot this data. Don't forget to call the `plt.show` function of matplotlib. The x-axis should have ticks from 1 to 31, and there should be a curve to each measuring station. Can you spot the weekends?

### Exercise 5.5 (best record company)

We use again the UK top 40 data set from the first week of 1964 in the `src` folder. Here we define "goodness" of a record company (`Publisher`) based on the sum of the weeks on chart (WoC) of its singles. Return a DataFrame of the singles by the best record company (a subset of rows of the original DataFrame). Do this with function `best_record_company`.

### Exercise 5.6 (suicide fractions)

Load the suicide data set from `src` folder. This data was originally downloaded from [Kaggle](https://www.kaggle.com/szamil/who-suicide-statistics). Kaggle contains lots of interesting open data sets.

Write function `suicide_fractions` that loads the data set and returns a Series that has the country as the (row) index and as the column the mean fraction of suicides per population in that country. In other words, the value is the average of suicide fractions. The information about year, sex and age is not used.

### Exercise 5.7 (suicide weather)

Copy the function `suicide fractions` from the previous exercise. 

Implement function `suicide_weather` as described below. We use the dataset of average temperature (over years 1961-1990) in different countries from `src/List_of_countries_by_average_yearly_temperature.html`([https://en.wikipedia.org/wiki/List_of_countries_by_average_yearly_temperature](https://en.wikipedia.org/wiki/List_of_countries_by_average_yearly_temperature)) . You can use the function `pd.read_html` to get all the tables from a html page. By default `pd.read_html` does not know which row contains column headers and which column contains row headers. Therefore, you have to give both `index_col` and `header` parameters to `read_html`. Make sure you use the country as the (row) index for both of the DataFrames. What is the [Spearman correlation](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient) between these variables? Use the `corr` method of Series object. Note the the two Series need not be sorted as the indices of the rows (country names) are used to align them.

The return value of the function `suicide_weather` is a tuple (suicide_rows, temperature_rows, common_rows, spearman_correlation) The output from the `main` function should be of the following form:

```llvm
Suicide DataFrame has x rows
Temperature DataFrame has x rows
Common DataFrame has x rows
Spearman correlation: x.x
﻿
```

You might have trouble when trying to convert the temperatures to float. The is because the negative numbers on that html page use a special _unicode minus sign_, which looks typographically nice, but the float constructor cannot interpret it as a minus sign. You can try out the following example:

```python
s="\u2212" "5"   # unicode minus sign and five
print(s)
try:
    float(s)
except ValueError as e:
    import sys
    print(e, file=sys.stderr)
        
﻿
```

`−5   ``could not convert string to float: '−5'`

But if we explicitly convert unicode minus sign to normal minus sign, it works:

```stylus
float(s.replace("\u2212", "-"))
```

-5.0

## Time series

If a measurement is made at certain points in time, the resulting values with their measurement times is called a time series. In Pandas a Series whose index consists of dates/times is a time series.

Let's make a copy of the DataFrame that we can mess with:

```abnf
wh2 = wh3.copy()
wh2.columns
```

Index(['Year', 'Month', 'Day', 'Time', 'Time zone', 'Precipitation', 'Snow',
       'Temperature'],
      dtype='object')

The column names `Year`, `Month`, and `Day` are now in appropriate form for the `to_datetime`function. It can convert these fields into a timestamp series, which we will add to the DataFrame.

```stylus
wh2["Date"] = pd.to_datetime(wh2[["Year", "Month", "Day"]])
wh2.head()
```

||Year|Month|Day|Time|Time zone|Precipitation|Snow|Temperature|Date|
|---|---|---|---|---|---|---|---|---|---|
|0|2017|1|1|00:00|UTC|-1.0|-1.0|0.6|2017-01-01|
|1|2017|1|2|00:00|UTC|4.4|-1.0|-3.9|2017-01-02|
|2|2017|1|3|00:00|UTC|6.6|7.0|-6.5|2017-01-03|
|3|2017|1|4|00:00|UTC|-1.0|13.0|-12.8|2017-01-04|
|4|2017|1|5|00:00|UTC|-1.0|10.0|-17.8|2017-01-05|

We can now drop the useless fields:

```stylus
wh2=wh2.drop(columns=["Year", "Month", "Day"])
wh2.head()
```

||Time|Time zone|Precipitation|Snow|Temperature|Date|
|---|---|---|---|---|---|---|
|0|00:00|UTC|-1.0|-1.0|0.6|2017-01-01|
|1|00:00|UTC|4.4|-1.0|-3.9|2017-01-02|
|2|00:00|UTC|6.6|7.0|-6.5|2017-01-03|
|3|00:00|UTC|-1.0|13.0|-12.8|2017-01-04|
|4|00:00|UTC|-1.0|10.0|-17.8|2017-01-05|

The following method call will set the Date field as the index of the DataFrame.

```abnf
wh2 = wh2.set_index("Date")
wh2.head()
```

||Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|
|Date||||||
|---|---|---|---|---|---|
|2017-01-01|00:00|UTC|-1.0|-1.0|0.6|
|2017-01-02|00:00|UTC|4.4|-1.0|-3.9|
|2017-01-03|00:00|UTC|6.6|7.0|-6.5|
|2017-01-04|00:00|UTC|-1.0|13.0|-12.8|
|2017-01-05|00:00|UTC|-1.0|10.0|-17.8|

We can now easily get a set of rows using date slices:

```subunit
wh2["2017-01-15":"2017-02-03"]
```

||Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|
|Date||||||
|---|---|---|---|---|---|
|2017-01-15|00:00|UTC|-1.0|8.0|-2.8|
|2017-01-16|00:00|UTC|-1.0|8.0|-4.2|
|2017-01-17|00:00|UTC|0.2|8.0|-3.5|
|2017-01-18|00:00|UTC|0.9|8.0|1.1|
|2017-01-19|00:00|UTC|-1.0|5.0|1.6|
|2017-01-20|00:00|UTC|0.3|5.0|-0.6|
|2017-01-21|00:00|UTC|0.4|5.0|-1.8|
|2017-01-22|00:00|UTC|0.2|5.0|1.0|
|2017-01-23|00:00|UTC|0.1|6.0|0.1|
|2017-01-24|00:00|UTC|-1.0|6.0|-2.2|
|2017-01-25|00:00|UTC|0.6|6.0|-3.8|
|2017-01-26|00:00|UTC|-1.0|6.0|1.9|
|2017-01-27|00:00|UTC|-1.0|4.0|1.6|
|2017-01-28|00:00|UTC|1.8|4.0|0.8|
|2017-01-29|00:00|UTC|2.6|3.0|0.6|
|2017-01-30|00:00|UTC|5.6|5.0|1.0|
|2017-01-31|00:00|UTC|-1.0|4.0|0.2|
|2017-02-01|00:00|UTC|1.5|4.0|-0.6|
|2017-02-02|00:00|UTC|0.2|5.0|-0.8|
|2017-02-03|00:00|UTC|-1.0|6.0|-0.2|

By using the `date_range` function even more complicated sets can be formed. The following gets all the Mondays of July:

```routeros
r=pd.date_range("2017-07-01", "2017-07-31", freq="w-mon")
r
```

DatetimeIndex(['2017-07-03', '2017-07-10', '2017-07-17', '2017-07-24',
               '2017-07-31'],
              dtype='datetime64[ns]', freq='W-MON')

```stylus
wh2.index.difference(r)
```

DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04',
               '2017-01-05', '2017-01-06', '2017-01-07', '2017-01-08',
               '2017-01-09', '2017-01-10',
               ...
               '2017-12-22', '2017-12-23', '2017-12-24', '2017-12-25',
               '2017-12-26', '2017-12-27', '2017-12-28', '2017-12-29',
               '2017-12-30', '2017-12-31'],
              dtype='datetime64[ns]', length=360, freq=None)

```stylus
wh2.loc[r,:]
```

||Time|Time zone|Precipitation|Snow|Temperature|
|---|---|---|---|---|---|
|2017-07-03|00:00|UTC|2.2|-1.0|14.5|
|2017-07-10|00:00|UTC|-1.0|-1.0|18.0|
|2017-07-17|00:00|UTC|2.7|-1.0|15.4|
|2017-07-24|00:00|UTC|-1.0|-1.0|15.7|
|2017-07-31|00:00|UTC|0.1|-1.0|17.8|

The following finds all the business days (Monday to Friday) of July:

```routeros
pd.date_range("2017-07-01", "2017-07-31", freq="b")
```

DatetimeIndex(['2017-07-03', '2017-07-04', '2017-07-05', '2017-07-06',
               '2017-07-07', '2017-07-10', '2017-07-11', '2017-07-12',
               '2017-07-13', '2017-07-14', '2017-07-17', '2017-07-18',
               '2017-07-19', '2017-07-20', '2017-07-21', '2017-07-24',
               '2017-07-25', '2017-07-26', '2017-07-27', '2017-07-28',
               '2017-07-31'],
              dtype='datetime64[ns]', freq='B')

We can get a general idea about the `Temperature` column by plotting it. Note how the index time series is shown nicely on the x-axis.

```scss
%matplotlib inline
wh2["Temperature"].plot();
```

[![Add alt](https://courses.mooc.fi/api/v0/files/course/af212a69-32b3-4c75-bb17-9cc850d99bf9/images/6d7ePzOdVphte7N6WYEed758LQuwTf.png)](https://courses.mooc.fi/api/v0/files/course/af212a69-32b3-4c75-bb17-9cc850d99bf9/images/6d7ePzOdVphte7N6WYEed758LQuwTf.png)

The graph looks a bit messy at this level of detail. We can smooth it by taking averages over a sliding window of length 30 days:

```routeros
rolling = wh2.Temperature.rolling(30, center=True)
rolling
```

```pgsql
Rolling [window=30,center=True,axis=0]
```

```stan
data = pd.DataFrame({"Temperature" : wh2.Temperature, "Rolling mean" : rolling.mean()})
data.plot();
```

[![Add alt](https://courses.mooc.fi/api/v0/files/course/af212a69-32b3-4c75-bb17-9cc850d99bf9/images/7kunJ6pRsF2etYhMp99PouKavzNZKl.png)](https://courses.mooc.fi/api/v0/files/course/af212a69-32b3-4c75-bb17-9cc850d99bf9/images/7kunJ6pRsF2etYhMp99PouKavzNZKl.png)

### Exercise 5.8 (bicycle timeseries)

Write function `bicycle_timeseries` that

- reads the data set
- cleans it
- turns its `Päivämäärä` column into (row) DatetimeIndex (that is, to row names) of that DataFrame
- returns the new DataFrame

### Exercise 5.9 (commute)

In function `commute` do the following:

Use the function `bicycle_timeseries` to get the bicycle data. Restrict to August 2017, group by the weekday, aggregate by summing. Set the `Weekday` column to numbers from one to seven. Then set the column `Weekday` as the (row) index. Return the resulting DataFrame from the function.

In the `main` function plot the DataFrame. Xticklabels should be the weekdays. Don't forget to call `show` function!

If you want the xticklabels to be `['Mon', 'Tue', 'Wed', 'Thu', 'Fr', 'Sat', 'Sun']` instead of numbers (1,..,7), then it may get a bit messy. There seems to be a problem with non-numeric `x` values. You could try the following after plotting, but you don't have to:

weekdays="x mon tue wed thu fri sat sun".title().split()  
plt.gca().set_xticklabels(weekdays)

## Additional information

[Pandas cheat sheet](https://github.com/pandas-dev/pandas/blob/master/doc/cheatsheet/Pandas_Cheat_Sheet.pdf) Summary of most important Pandas' functions and methods.

Read the article [Tidy Data](https://www.jstatsoft.org/article/view/v059i10/v59i10.pdf). The article uses the statistical software R as an example, but the ideas are relevant in general. Pandas operations maintain data in the tidy format.

Pandas handles only one dimensional data (Series) and two dimensional data (DataFrame). While you can use [hierarchical indices](http://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html#hierarchical-indexing-multiindex) to simulate higher dimensional arrays, you should use the [xarray](http://xarray.pydata.org/en/stable/index.html) library, if you need proper higher-dimensional arrays with labels. It is basically a cross between NumPy and Pandas.