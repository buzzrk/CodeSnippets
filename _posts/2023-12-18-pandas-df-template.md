## Template for dataframe manipulation

```
result = (mydf
          [
            [   col for col in mydf.columns
                 if ("" in col or "s" in col) 
            ]
           ] 
          .select_dtypes(['integer','float','object'])
          .groupby('city')
          .agg(
               {'rainfall': 'sum',
                'population': 'avg',
                 'snow':'sum'}
          )
          .assign(
            avgsnow  = lambda df: df['snow'] / df['pop'],
            avgrainfall = lambda df: df['rainfall'] / df['pop']
          )
          .reset_index()
          #.query(' `avgrainfall`>=10 & `avgsnow`.notna() ')
          .sort_values('avgrainfall', ascending=False))
display(result)
```
