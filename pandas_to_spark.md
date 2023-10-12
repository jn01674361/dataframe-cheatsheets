# Pandas to PySpark DataFrame Cheat Sheet

Transitioning from pandas to PySpark? Here's a quick guide on how common operations compare.

## 1. **Creating a DataFrame**

### Pandas
```python
import pandas as pd

df = pd.DataFrame({'A': range(5), 'B': range(5)})
```

### PySpark
```python
from pyspark.sql import SparkSession
from pyspark.sql import Row

spark = SparkSession.builder.appName("example").getOrCreate()

data = [Row(A=i, B=i) for i in range(5)]
df = spark.createDataFrame(data)
```

## 2. **Reading from CSV**

### Pandas
```python
df = pd.read_csv('filename.csv')
```

### PySpark
```python
df = spark.read.csv('filename.csv', header=True, inferSchema=True)
```

## 3. **Filtering Data**

### Pandas
```python
df_filtered = df[df['A'] > 2]
```

### PySpark
```python
df_filtered = df.filter(df['A'] > 2)
```

## 4. **Groupby Operations**

### Pandas
```python
grouped = df.groupby('A').sum()
```

### PySpark
```python
grouped = df.groupBy('A').sum()
```

## 5. **Setting Index (PySpark has no direct equivalent, but you can sort)**

### Pandas
```python
df = df.set_index('A')
```

### PySpark
```python
df = df.orderBy('A')
```

## 6. **Getting Unique Values**

### Pandas
```python
unique_vals = df['A'].unique()
```

### PySpark
```python
unique_vals = df.select('A').distinct()
```

## 7. **Value Counts**

### Pandas
```python
val_counts = df['A'].value_counts()
```

### PySpark
```python
val_counts = df.groupBy('A').count()
```

## 8. **Applying Functions**

### Pandas
```python
df['B'] = df['A'].apply(lambda x: x**2)
```

### PySpark (using UDF)
```python
from pyspark.sql.functions import udf
from pyspark.sql.types import IntegerType

squared = udf(lambda x: x**2, IntegerType())
df = df.withColumn('B', squared(df['A']))
```

## 9. **Merging DataFrames**

### Pandas
```python
merged_df = pd.merge(df1, df2, on='A')
```

### PySpark
```python
merged_df = df1.join(df2, df1['A'] == df2['A'])
```

## 10. **Computing Descriptive Statistics**

### Pandas
```python
mean_val = df['A'].mean()
```

### PySpark
```python
mean_val = df.select('A').groupBy().avg().collect()[0][0]
```

## 11. **Writing to CSV**

### Pandas
```python
df.to_csv('output.csv', index=False)
```

### PySpark
```python
df.write.csv('output.csv', header=True)
```

