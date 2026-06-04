
[[dev-notes]]
[[html2pdf]]

[[pip differences]]

## uv
	use uv for package and venv features
```bash
uv init
uv add numpy>=2.0
uv run myscript.py

uv run --with jupyter jupyter lab

uv sync #import pyproject.toml
uv python pin 3.12.9
uvx --from jupyter-core jupyter lab ## quick, ephemoral?

```

### pyproject.toml
```toml
[project]
name = "my_project"
version = "1.0.0"
requires-python = ">=3.9,<3.13"
dependencies = [
  "astropy>=5.0.0",
  "pandas>=1.0.0,<2.0",
]
```

## pip
```bash
pip install jupyterlab
pip install numpy
pip install pandas
pip install matplotlib
pip install seaborn
pip install pandasql
```

```Python
# python recursive factorial
def factorial(num):
	if num == 1 or num == 0:
		return 1
	else:
		return (num * factorial(num-1))
		
factorial(5)
```

```python
main_string = "Hello, world!"
substring = "world"
if substring in main_string:
    print("Substring found!")
else:
    print("Substring not found.")
```

```python
# boot.dev median solution
def median_followers(nums):
    if len(nums) == 0:
        return None
    nums = sorted(nums)
    n = len(nums)
    if n % 2 == 0:
        return (nums[n // 2 - 1] + nums[n // 2]) / 2
    return nums[n // 2]
# my solution
def median_followers(nums):
    if not nums:
        return None
    nums = sorted(nums)
    if len(nums) % 2 == 0:
        left = nums[int((len(nums)/2)-1)]
        right = nums[int((len(nums)/2))]
        return ((left + right)/2) 
    else:
        return nums[int((len(nums)/2)-.5)]
      
```

```python
class Student:
    def __init__(self, name):
        self.name = name
        self.__courses = {}

    def calculate_letter_grade(self, score):
        if score >= 90:
            return "A"
        elif score >= 80 and score < 90:
            return "B"
        elif score >= 70 and score < 80:
            return "C"
        elif score >= 60 and score < 70:
            return "D"
        else:
            return "F"

    def add_course(self, course_name, score):
        self.__courses[course_name] = self.calculate_letter_grade(score)

    def get_courses(self):
        return self.__courses

```
### unique python features

```python
#python floor divide operator
print(3//2) # 1
```
### pandas
```Python
prev90[prev90['Grade'].isna()]
#return rows wil null values
df.info () # Information about the DataFrame
df.describe () # Summary statistics
```

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme()

pd.set_option('display.max_columns', 20) #replace n with the number of columns you want to see completely
pd.set_option('display.max_rows', 500) #replace n with the number of rows you want to see completely
pd.set_option('display.max_colwidth', 40)
```
#### dtypes
- Numeric:
    - `int64`
    - `float64`
- Text:
    - `object` (often used for strings)
    - `StringDtype`
- Boolean:
    - `bool`
    - `BooleanDtype`
- Date/Time:
    - `datetime64[ns]`
    - `timedelta[ns]`
    - `Period`
- Categorical:
    - `category`
- Other:**
    - `Sparse`
    - `Interval`
    - `Int64Dtype`
    - `Float64Dtype`

### matplotlib
```python
import matplotlib.pyplot as plt

# Plot some data
plt.plot(['a', 'b', 'c'], [4, 8, 1])

# Set the title and labels
plt.title("Example Plot")
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
#blanks
plt.plot()
plt.title()
plt.ylabel()
plt.xlabel()

# Save the plot to a file (e.g., PNG)
plt.savefig("example_plot.png")
```


# Code Snippets

```
   ____                                    _
  / ___|___  _ __  _   _   _ __   __ _ ___| |_ __ _
 | |   / _ \| '_ \| | | | | '_ \ / _` / __| __/ _` |
 | |__| (_) | |_) | |_| | | |_) | (_| \__ \ || (_| |
  \____\___/| .__/ \__, | | .__/ \__,_|___/\__\__,_|
            |_|    |___/  |_|

```
## imports
```python

import sys
sys.path.append('../integration/')
import nsconnect
import sheets
creds = sheets.connect()

result = sheets.create_many("duplicate contacts upload",df_list,creds)
result
```

```python

if __name__ == "__main__":
    main()

```

## Utility Functions Utils
```python

def ts():
    return pd.Timestamp.now().strftime('%Y_%m_%d_%H:%M:%S')

def read_file(file_path):
    with open(file_path, 'r') as file:
        return file.read()

def to_csv(name, df):
    file_path = f"../../analysis/{name}.csv"
    df.to_csv(file_path, index=False)
    print(f"Output saved to {file_path}")


```

## sqlite
```python
import sqlite3
import time

sqlite_conn = sqlite3.connect("logs.db")
sqlite_cursor = sqlite_conn.cursor()
sqlite_cursor.execute("CREATE TABLE IF NOT EXISTS logs (message TEXT, time real)")


def log(message):
    sqlite_cursor.execute("INSERT INTO logs VALUES (?, ?)", (message,time.time()))
    print(message)

log("starting")

sqlite_conn.commit()
sqlite_cursor.close()

```

## boilerplate
```python
import pandas as pd
pd.set_option('display.max_columns', 50)
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_colwidth', 140)
pd.options.mode.copy_on_write = True
pd.options.display.float_format = '{:20,.2f}'.format

import numpy as np

import matplotlib.pyplot as plt
plt.style.use('dark_background')

import seaborn as sns
sns.set_theme()

import hvplot.pandas

from thefuzz import fuzz 
from thefuzz import process 

```

## run command to import other notebooks or py files

```python
%run ~/data/programs/utils/utils.py
```

## auto reload imports
```python
%load_ext autoreload
%autoreload 2

importing from subdirectoies

import sys
sys.path.append('/path/to/your/directory')
import mymodule

```

### logging python webscraper scripts

### bash script to monitor logs
```python
truncate -s 0 scraper.log && watch -n 1 "cat scraper.log | tail -n 20"

## count of unique
sales_order_qty_terr = sales_orders["tranID"].nunique()

#START pandas code snippets
# code snippets for copy pasta
# # reset index and drop column example from  /sales/invoiced/legacy...
tmp_df = tmp_df.reset_index().drop("index", axis=1)

# sort
new_df.sort_values('Sales Amount', ascending=False)

## pivot tables

### Pandas aggfunc options
    # sum: Calculates the sum of the values in the specified column(s).
    # mean: Calculates the mean (average) of the values in the specified column(s).
    # median: Calculates the median (middle value) of the values in the specified column(s).
    # min: Returns the minimum value in the specified column(s).
    # max: Returns the maximum value in the specified column(s).
    # count: Counts the number of values in the specified column(s).
    # std: Calculates the standard deviation of the values in the specified column(s).
    # var: Calculates the variance of the values in the specified column(s).
# pivot
tmp_pivot = pd.pivot_table(tmp_df, index='Item', values='Amount', aggfunc='sum').sort_values('Amount', ascending=False).reset_index()

## working with NAN

# working with NAN
df = df.fillna('')
# remove nan from df
df = df[df['column'].notna()]
df = df[df['column'].isnull()]

## changing and importing types

df = df.astype(object)
df = pd.read_csv('my_data.csv',dtype = {'col1': str, 'col2': float, 'col3': int})

## pandas columns

### rename columns

#rename column
df = df.rename(columns={'old_column_name': 'new_column_name'})

### uppercase pandas column

sales["Item"] = sales["Item"].str.upper()

### to datetime

df['Date'] = pd.to_datetime(df['Date'])

## datetime

tmp_df = df[df['Date'].dt.year == year]

df = df.sort_values(by='Date', ascending=False)
x = str(list(customer_df['Date'])[0])
x = x.removesuffix(' 00:00:00')

# filter using datetime
invoices.loc[(invoices['Date'] >= f"{year}-01-01") & (invoices['Date'] <= f"{year}-12-31")]
# end date time

test = pd.DataFrame({
    "record":[1, 2, 3, 4],
    "AUE Date":["6/1/2027", "6/1/2027", "6/1/2023", "6/1/2027"]
})
test
test["AUE Date"] = pd.to_datetime(test["AUE Date"], format="%m/%d/%Y")
test = test.sort_values('AUE Date', ascending=False)
testlist = list(test["AUE Date"])
testlist
round(pd.Timedelta(testlist[0] - testlist[-1]).days / 365, 3)

test



import datetime
from datetime import timedelta

def get_previous_month():
    today = datetime.datetime.now()
    first_day_current_month = today.replace(day=1)
    last_day_previous_month = first_day_current_month - timedelta(days=1)
    return last_day_previous_month.strftime('%B')


last_month = get_previous_month()
last_month



## group and join values into one

similar to textjoin and filter in google sheets

df['branch'] = df.groupby(['Name'])['branch'].transform(lambda x : ' '.join(x))

import datetime

print(datetime.date(2010, 5, 24))

# datetime.datetime.strptime('24052010', "%d%m%Y").date()
datetime.datetime.strftime('24052010', "%d%m%Y")


type

## JSON

# JSON
bomjson = json.dumps(no_refurb_boms)
parse_sample = json.loads(sample)

## duplicates

def return_dups(df):
    return df[df["Name"].duplicated(keep=False)]

dups = df[df["Name"].duplicated(keep=False)] # False marks all duplicates as True

df.drop_duplicates(subset=['brand'])

def find_empty_columns(df):
    colname = []
    colval = []
    cols = list(df.columns) 
    for col in cols:
        val = list(df[col].unique())
        if len(val) > 1:
            colval.append(val)
            colname.append(col)
    return pd.DataFrame({"col": colname, "val":colval})

res = find_empty_columns(upload_contacts)
res

## mixed bag

sliced_dict = {key: dict[key] for key in keys_to_extract}

df['A'] = df['A'].astype(float)


df['Item'] = df['Item'].apply(lambda x: extract(x))

items = items[(items["Type"]=="Inventory Item") | (items["Type"] == "Assembly")]

# selecting multiple columns
items[['Description', 'Name']]

## both sort and reset
tmp_df = df[df['item_id'] == item_id]
tmp_df = tmp_df.sort_values('AUE Date', ascending=False)
tmp_df = tmp_df.reset_index().drop("index", axis=1)
tmp_df.loc[i, 'AUE Date'] = value

# removes duplicate from list
sales_customer_list = list(set(list(sales.Customer)))

# removes nans from list
clean_sales_customer_list = [x for x in sales_customer_list if str(x) != 'nan']

# remove 0 from list
X = [0,5,0,0,3,1,15,0,12]
X = [i for i in X if i != 0]

# concat dataframes
new_df = pd.concat([new_df, customer_df])

df.info () # Information about the DataFrame
df.describe () # Summary statistics
now = pd.Timestamp.now().strftime('%Y_%m_%d_%H:%M:%S')

df.set_index('Name', inplace=True)

analysis = sales_peaks.join(reverse_boms)

reverse_boms.set_index("Item", inplace=True)

reverse_boms.drop(columns="Unnamed: 0", inplace=True)

df.rename(columns={'old_name': 'new_name'}, inplace=True)

df['new_column'] = df.index

temp_boms = json.dumps(list(temp_df['Bill of Materials : Name']))
parse_sample = json.loads(sample)

# turn a percent string into a float '5%' => 0.05
analysis['90 Day vs. 365 Day'] = analysis['90 Day vs. 365 Day'].str.replace('%', '').astype(float)/100
# turns a float into a percent string 0.05 => '5%'
analysis['90 Day vs. 365 Day'] = analysis['90 Day vs. 365 Day'].map('{:.2%}'.format)


df.insert(1, "new_column", [value1, value2, value3])


df['new_column'] = df['column1'] * df['column2']


plt.rcParams['figure.figsize'] = [22, 10]


filtered_df = df.loc[(df['date'] >= start_date) & (df['date'] <= end_date)]

chart = chart.loc[(chart['Date'] >= pd.to_datetime(start_date)) & (chart['Date'] <= pd.to_datetime(end_date))]

aue_key["chromebook"] = aue_key["chromebook"].str.upper()


test["date"] = pd.to_datetime(test["date"], format="%m/%d/%Y")

repair_breakdown_2024= repair_breakdown_2024.round({'Avg Invoice Amount':2})

    try:
          # Code that might raise an exception
    except SomeException:
          # Code to handle the exception
    else:
         # Code to run if no exception occurs
    finally:
        # Code to run regardless of whether an exception occurs

import pandas as pd
import numpy as np

# Sample data
df = pd.DataFrame({
    'target_column': ['A', np.nan, 'C', 'C', np.nan],
    'source_column': ['X', 'Y', 'Z', 'W', 'V']
})

# Fill NaN/None values only
df['target_column'] = df['target_column'].fillna(df['source_column'])

df

df['Mean_Column'] = df.mean(axis=1)

def check_number(x):
    match x:
        case 10:
            print("It's 10")
        case 20:
            print("It's 20")
        case _:
            print("It's neither 10 nor 20")

check_number(10)
check_number(30)

## find empty columns

def find_empty_columns(df):
    colname = []
    colval = []
    cols = list(df.columns) 
    for col in cols:
        val = list(df[col].unique())
        if len(val) > 1:
            colval.append(val)
            colname.append(col)
    return pd.DataFrame({"col": colname, "val":colval})

res = find_empty_columns(upload_contacts)
res

## everything else

dataframe.fillna({'Count':'Unknown', 'Name': 'GFG'}, inplace=True)


```


## Functions

```python
# START convert kit skus
def create_new_item_sku(f):
    def extract(x):
            if x[-1] not in ['1','2','3','4','5','6','7','8','9','0']:
                return x
            else:
                if x[-2] == '-':
                    return x[0:-2]
                elif x[-3] == '-':
                    return x[0:-3]
                else:
                    return x
    df['Item'] = df['Item'].apply(lambda x: extract(x))
    return df
def g_remover(df):
    def g_extract(x):
        if x[0] == 'G' and x[1] == '-':
            return x[2:]
        else:
            return x
    df['Item'] = df['Item'].apply(lambda x: g_extract(x))
    return df
def convert_kit_skus(x):
    df = x.copy()
    df['Kit SKU'] = df['Item']
    df = create_new_item_sku(df)
    df = g_remover(df)
    return df
    print('cleaned item skus...')
# END convert kit skus
```



```python
def filter_df_date(df, year, start_month, end_month):
    df = df[df['Date'].dt.year == year]
    df = df[(df['Date'].dt.month >= start_month) & (df['Date'].dt.month <= end_month)]
    return df

def ts():
    return pd.Timestamp.now().strftime('%Y_%m_%d_%H:%M:%S')

# export output utility function
def ts_export(output, name):
    now = pd.Timestamp.now().strftime('%Y_%m_%d_%H:%M:%S')
    output.to_csv(f'../../analysis/{name}_{now}.csv')
    print('exported the output to csv...')
    print('filepath')
    print(f'../analysis/{name}_{now}.csv')

# converts $ column into number
## column is a string
def convert_to_number(df, column):
    df[column] = df[column].str.replace('$','').str.replace(',','').astype(float)
## end covert to number code block

# # iterrows example from /sales/invoiced/legacy...
def margin_calculator(df):
    for i, row in df.iterrows():
        value = row["Rate"] - row["avg-cost"]
        df.loc[i, "margin"] = value
    print("margin calculated...")

# d = {'Rate': [10, 20, 5], 'avg-cost': [3.5, 4, 15]}
# df = pd.DataFrame(data=d)
# margin_calculator(df)
# df

export = False
# export = True
if export == True:
    output.to_csv(f'../analysis/{name}_{now}.csv')
    print('exported the output to csv...')
else:
    print('no export')
print('filepath')
print(f'../analysis/{name}_{now}.csv')
# output.dtypes
# output.shape
# output.columns
# output.loc[9]
# output.head(30)
# output.head(3)
# output

# output = find_customer_invoices(invoices_df, cust_list)
# output.head(3)

# # scan two lists 
# output = nscanner(ns_list, new_list)

#begin customer scanner program 'nscanner'
# given a list of customer names this function will return fuzzy matches and includes options to remove selected Terms
# dependencies: pandas, fuzzywuzzy
def nscanner(ns_list, new_list):
    slim_leads=[]
    slim_custs=[]
    lead_list=[]
    cust_list=[]
    for lead in new_list:
        # business commons
        # commons = ['Inc.','Inc','Associates','Corporation', 'Services', 'Technologies','Technology','Computer', 'Computers', 'Communications', 'International', 'Solutions']
        # school commons
        # commons = ['Regional','County','Public','Schools','District','United','School','Community']
        commons=[]
        slim_lead = lead
        try:
            for x in commons:
                slim_lead = slim_lead.replace(x,'').strip()
        except:
            print("lead", lead)
        for cust in ns_list:
            slim_cust = cust
            try:
                for x in commons:
                    slim_cust= slim_cust.replace(x,'').strip()
            except:
                print("cust",cust)
            try:
                if fuzz.ratio(slim_lead, slim_cust) > 70:
                    slim_leads.append(slim_lead)
                    slim_custs.append(slim_cust)
                    lead_list.append(lead)
                    cust_list.append(cust)
            except:
                print("fuzzy",slim_lead, cust)
    return pd.DataFrame({'slim_leads': slim_leads,'slim_custs':slim_custs,'leads': lead_list, 'ns customers': cust_list})
## end nscanner block

# begin find customer invoice block
# given invoices data frame and a list of customer ids 
# this function will scan the dataframe for customers matching 
# and return a new dataframe with the customers on the list
# # find all invoices by customer
# invoices_df = import_csv('/sales/find invoices by customer/input/invoices_(22-24)_10_23_24')
# cust_df = import_csv('/sales/find invoices by customer/input/kens_list')
# cust_list = list(cust_df['Internal ID'])
# 
def find_customer_invoices(invoices_df, cust_id_list):
    new_df = pd.DataFrame()
    for cust_id in cust_id_list:
        tmp_df = invoices_df[invoices_df['Customer Internal ID'] == cust_id]
        new_df = pd.concat([new_df, tmp_df])
    return new_df

## Linear Regression

import numpy as np
from scipy import stats
import pandas as pd

# Example data
x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 5, 4, 5])

# Method 1: Using scipy.stats
slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)
print(f"Slope: {slope}")

# Method 2: Using numpy's polyfit
slope_np = np.polyfit(x, y, 1)[0]
print(f"Slope (numpy): {slope_np}")

# Method 3: Using pandas and statsmodels
import statsmodels.api as sm

df = pd.DataFrame({'x': x, 'y': y})
model = sm.OLS(df['y'], sm.add_constant(df['x'])).fit()
slope_sm = model.params[1]
print(f"Slope (statsmodels): {slope_sm}")
```

3. Considerations

- **Multiple Variables**: For multivariate data, consider multiple regression
- **Non-linear Relationships**: Linear slope may not be appropriate if your data follows a non-linear pattern
- **Outliers**: Can significantly affect slope calculations - consider robust regression methods
- **Data Quality**: Ensure your x and y values are properly paired and make logical sense

Remember that the slope is only meaningful as a representation of your data if a linear relationship is appropriate for your dataset.



