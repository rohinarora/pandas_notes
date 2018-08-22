
  len(df)     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;           series + value &nbsp;&nbsp;&nbsp;&nbsp;   df[df.c == value]     
  df.head()  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  series + series2 &nbsp; df[(df.c >= value) & (df.d < value)]     
  df.tail()  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   series.notnull() &nbsp;&nbsp;&nbsp; df[(df.c < value) | (df.d != value)]     
  df.COLUMN  &nbsp;&nbsp;   series.isnull()  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; df.sort_values('column')     
  df['COLUMN']  series.order() &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   df.sort_values(['column1', 'column2'])      

 * s=series

  s.str..... -> all string methods can be applied on pandas series having strings       

  s.str.len()    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    s.value_counts() df[['column1', 'column2']]     
  s.str.contains()  &nbsp; s.sort_index() &nbsp;&nbsp;&nbsp; df.plot(x='a', y='b', kind='scatter')     
  s.str.startswith()  s.plot(...)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    df.plot(x='a', y='b', kind='bar')      


  df.set_index('a').sort_index()        df.loc['value']     
  df.set_index(['a', 'b']).sort_index() df.loc[('v','u')]    df.loc['v'].loc['u']     
  df.reset_index('a') df.reset_index(['a','b'])    
  df.groupby('column')                  .size() .mean() .min() .max()     
  df.groupby(['column1', 'column2'])    .agg(['min', 'max'])     


  df.unstack()      s.dt.year     
  df.stack()        s.dt.month    
  df.fillna(value)  s.dt.day   
  s.fillna(value)   s.dt.dayofweek   





dataframe consists of columns, index and values

> df=pd.read_csv('....')

each of the following function can be used to explore the dataframe

> index = df.index   # index object
> columns = df.columns  # index object
> data = df.values   # numpy object
> series.value
> series.index
> series.coloumns


> type(index)
pandas.core.indexes.range.RangeIndex

> type(columns)      #  we would refer to the columns as a pandas Index object.
pandas.core.indexes.base.Index

> type(data)
numpy.ndarray

 The output of the columns attribute appears to be just a sequence of the column names. This sequence of column names is technically an Index object.

The built-in subclass function checks whether the first argument inherits from the second.

> issubclass(pd.RangeIndex, pd.Index)
True

Essentially, the index and the columns represent the same thing, but along different axes. They’re occasionally referred to as the row index and column index.

In this context, the Index objects refer to all the possible objects that can be used for the index or columns. They are all subclasses of pd.Index. Here is the complete list of the Index objects: CategoricalIndex, MultiIndex, IntervalIndex, Int64Index, UInt64Index, Float64Index, RangeIndex, TimedeltaIndex, DatetimeIndex, PeriodIndex.


A RangeIndex is a special type of Index object that is analogous to Python's range object. Its entire sequence of values is not loaded into memory until it is necessary to do so, thereby saving memory. It is completely defined by its start, stop, and step values.


By default the term index refers to all the index labels as a whole just as the term columns refers to all the column names as a whole.

When multiple Series or DataFrames are combined, the indexes align first before any calculation occurs. Collectively, the columns and the index are known as the axes.  

A DataFrame has two axes--a vertical axis (the index) and a horizontal axis(the columns). Pandas borrows convention from NumPy and uses the integers 0/1 as another way of referring to the vertical/horizontal axis.


Beneath the index, columns, and data are NumPy ndarrays. They could be considered the base object for pandas that many other objects are built upon.
All the following are numpy ndarray objects-

df.columns.values
df.index.values
df.values

# Pandas datatypes  reference http://pandas.pydata.org/pandas-docs/stable/basics.html#dtypes

Each DataFrame column must be exactly one type. The object data type is the one data type that is unlike the others. A column that is of object data type may contain values that are of any valid Python object. The object data type is a catch-all for columns that pandas doesn’t recognize as any other specific type.

Pandas datatypes non trivial-
1. Object      np.object       aka - O, object
Typically strings but is a catch-all for columns with multiple different types or other Python objects (tuples, lists, dicts, and so on).

2. Datetime

3. Timedelta

4. Categorical     pd.Categorical     aka - category
Specific only to pandas. Useful for object columns with relatively few unique values.



df.dtypes()
df.get_dtype_counts()


using the dot notation to access columns should be avoided with production code.


In a Jupyter notebook, when holding down Shift + Tab + Tab with the cursor placed somewhere in the object, a window of the docsstrings will pop out making the method far easier to use. This intelligence again disappears if you try to chain an operation after selecting a column with the indexing operator.

It is possible to turn this Series into a one-column DataFrame with the to_frame method. This method will use the Series name as the new column name


To understand how Python objects gain the capability to use the indexing operator, see the Python documentation on the __getitem__ special method (http://bit.ly/2u5ISN6)



>pd.describe()
>pd.series.describe()
>pd.series.value_counts()
>pd.series.value_counts(normalize=True)
>pd.series.hasnans
>pd.series.isnull()
>pd.series.notnull()
>pd.series.fillna(0)
>pd.series.dropna(0)
other methods- count, size, shape, unique()

>pd.series.plot(kind='...') -> plots index on x axis and values on y axis

pd.series.str.  -> all string methods apply if series has strings as values

> pd.set_index('')
or directly-
> pd.read_csv('......csv', index_col='....')

^ By default, both set_index and read_csv drop the column used as the index from the DataFrame. With set_index, it is possible to keep the column in the DataFrame by setting the drop parameter to False.

> pd.reset_index('')


# renaming DF

The rename DataFrame method accepts dictionaries that map the old value to the new value.

> df_renamed = df.rename(index=idx_rename,columns=idx_rename)
  where idx_rename and idx_rename are dictionaries

  or use to_list-

>  df_old_index=df.index.to_list()
>  df_new_index=function(df_old_index)
>  df.index=df_new_index

>  df_old_coloumn=df.coloumns.to_list()
>  df_new_index=function(df_old_index)
>  df.index=df_new_index


# deleting from df

>df.drop('....',axis='columns')
or
>df.drop('....',axis=1)


# insert coloumn in a specific location

* The insert method
*  use the get_loc Index method to find the integer location of the column name.
* The insert method modifies the calling DataFrame in-place, so there won't be an assignment statement. lowing:

> index_integer = df.columns.get_loc('gross') + 1
> df.insert(loc=index_integer, column=<coloumn_name>, value=df['gross'] - df['budget'])


q. sort_values vs sort_index
http://pandas.pydata.org/pandas-docs/stable/whatsnew.html#changes-to-sorting-api
sort_values is meant to sort by the values of columns
sort_index is meant to sort by the index labels (or a specific level of the index, or the column labels when axis=1)

sort_values can be applied directly on a series, or a dataframe (passing the coloumn in brackets of Df)


index is like magic. The Index component of the Series and DataFrame is what separates pandas from most other data analysis libraries and is the key to understanding how many operations work

functions on series/df often return series/df which allows "method chaining"

pd.Series.map(....)  -> very good



Pandas resources

https://twitter.com/tedpetrou/status/920648815761178625
 - book downloaded on ubuntu

https://twitter.com/tedpetrou/status/939252987473489920


pd.set_option('display.max_columns', None)  
jupyter notebook --NotebookApp.iopub_data_rate_limit=10000000

Pandas

pd.read_table   assumes tab as delimiter
pd.read_csv   - assumes , as delimited
header=none if no header present. pass custom header via name=“”. header=0 if header present and we want to replace it. or just leave blank coz header=0 is default

pd.read_table(sep=,) is equivalent to pd.read_csv

pd.describe(include=‘’)  | some data type. only that data type will be described then
pd.shape
pd.drop (#index name#). this index can be row or column index

df.rename(columns=lambda x: x.replace(' ', '_'), inplace=True)
df.rename(columns=lambda x: '_'.join([x.strip() for x in x.lower().split()]), inplace=True)


speed up pandas
https://www.youtube.com/watch?v=HN5d490_KKk
