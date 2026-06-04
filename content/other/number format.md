If you want to prevent Pandas from displaying numbers in scientific notation, you can adjust the display settings. Here are a few methods to achieve this:

### Method 1: Set Display Options
You can set the display option for floating-point numbers to a fixed format using the following code:

```python
import pandas as pd

# Set display option to show float numbers in fixed format
pd.set_option('display.float_format', '{:.2f}'.format)
```

This will format floating-point numbers to two decimal places. You can adjust the number of decimal places by changing the `2` in `'{:.2f}'` to your desired value.

### Method 2: Convert to String
If you want to convert the numbers to strings to avoid scientific notation, you can use the `astype` method:

```python
df['column_name'] = df['column_name'].astype(str)
```

Replace `'column_name'` with the name of the column you want to convert.

### Method 3: Use `round()`
If you want to round the numbers to a specific number of decimal places without changing the display settings, you can use the `round()` method:

```python
df['column_name'] = df['column_name'].round(2)
```

### Method 4: Use `format` in Output
When printing or displaying the DataFrame, you can format the output directly:

```python
print(df.to_string(formatters={'column_name': '{:.2f}'.format}))
```

Choose the method that best fits your needs!