## Template for dataframe manipulation

* Select columns by column name
* Select columns by data types
* Aggregate
* Create new columns
* Filter
* Sort


```
import pandas as pd
# Mock data
data = {
    'city': ['New York', 'New York', 'Chicago', 'Chicago', 'Chicago'],
    'population': [8537673, 3976322, 2704958, 2303482, 1680992],      
    'rainfall': [45.7, 14.9, 36.7, 49.8, 8.0],
    'snow': [4.7, 1.9, 3.7, 4.8, 8.0]
}
# Creating DataFrame
mydf = pd.DataFrame(data)

result = (mydf
          [
            [   col for col in mydf.columns
                if ( "" in col
                    or
                    "s" in col
                ) 
            ]
           ] 
          #.select_dtypes(['integer','float','object'])
          .groupby(['city'])
          .agg(
               {'rainfall': 'sum',
                'snow': 'sum',
                'population': 'mean',
                }
          )
          .assign(
            avgsnow  = lambda df: df['snow'] / df['population'],
            avgrainfall = lambda df: df['rainfall'] / df['population']
          )
          .reset_index()
          .query(' `avgrainfall`>=0 & `avgsnow`.notna() ')
          .sort_values('avgrainfall', ascending=False))
display(result)
```
