## How to show data as tables in jupyter notebook

```
result = (mydf
          [[col for col in mydf.columns if ("" in col or "s" in col)]]  #get subset of columns based on condition
          .select_dtypes(['integer','float','object']) # filter by data type
          .groupby('city')
          .agg({'rainfall': 'sum', 'population': 'average','snow':'sum'})
          .assign( avgsnow  = lambda df: df['snow'] / df['population']
                  ,avgrainfall = lambda df: df['rainfall'] / df['population']
                 )
          .reset_index()
          #.query(' `avgrainfall`>=10 & `avgsnow`.notna() ')
          .sort_values('avgrainfall', ascending=False))
display(result)
```
