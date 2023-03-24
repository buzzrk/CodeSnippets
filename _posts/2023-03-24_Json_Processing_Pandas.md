## Pandas Tricks for processing json with nested and repeated fields

### Load json into dataframe
```
import pandas as pd
import json as json
from pandas.io.json import json_normalize

with open('data.json', 'w') as f:
    json.dump(data, f)
d1 = pd.json_normalize(data,errors='ignore')
```

### Split repeated data in column to new rows

```
df = df.explode("columnname")
```

### Split nested Column into column

```
def split_json_columns(df, column_name):
    df.reset_index(drop=True, inplace=True)
    df_new = pd.json_normalize(df[column_name])
    df_new.reset_index(drop=True, inplace=True)
    df_new.columns = [column_name + "_"+ str(x) for x in df_new.columns]
    df_return = pd.concat([df,df_new],axis=1).drop(column_name,axis=1)
    df_return.reset_index(drop=True, inplace=True)
    return df_return
df = split_json_columns(df,"columnname")
```
