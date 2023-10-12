## 1. **Creating a DataFrame**

### Pandas
```python
import pandas as pd

df = pd.DataFrame({'A': range(5), 'B': range(5)})
```

### Dask
```python
import dask.dataframe as dd

ddf = dd.from_pandas(df, npartitions=2)
```
Or directly:
```python
ddf = dd.from_array({'A': range(5), 'B': range(5)}, chunksize=2)
```

## 2. **Reading from CSV**

### Pandas
```python
df = pd.read_csv('filename.csv')
```

### Dask
```python
ddf = dd.read_csv('filename.csv')
```

## 3. **Filtering Data**

### Pandas
```python
df_filtered = df[df['A'] > 2]
```

### Dask
```python
ddf_filtered = ddf[ddf['A'] > 2]
```

## 4. **Groupby Operations**

### Pandas
```python
grouped = df.groupby('A').sum()
```

### Dask
```python
grouped = ddf.groupby('A').sum().compute()
```

## 5. **Setting Index**

### Pandas
```python
df = df.set_index('A')
```

### Dask
```python
ddf = ddf.set_index('A').compute()
```

## 6. **Getting Unique Values**

### Pandas
```python
unique_vals = df['A'].unique()
```

### Dask
```python
unique_vals = ddf['A'].unique().compute()
```

## 7. **Value Counts**

### Pandas
```python
val_counts = df['A'].value_counts()
```

### Dask
```python
val_counts = ddf['A'].value_counts().compute()
```

## 8. **Applying Functions**

### Pandas
```python
df['B'] = df['A'].apply(lambda x: x**2)
```

### Dask
```python
ddf['B'] = ddf['A'].map(lambda x: x**2).compute()
```

## 9. **Merging DataFrames**

### Pandas
```python
merged_df = pd.merge(df1, df2, on='A')
```

### Dask
```python
merged_ddf = dd.merge(ddf1, ddf2, on='A').compute()
```

## 10. **Computing Descriptive Statistics**

### Pandas
```python
mean_val = df['A'].mean()
```

### Dask
```python
mean_val = ddf['A'].mean().compute()
```

## 11. **Writing to CSV**

### Pandas
```python
df.to_csv('output.csv', index=False)
```

### Dask
```python
ddf.to_csv('output-*.csv', index=False)  # Produces multiple part files
```
