

Given timestamps of logins, figure out how many people on Facebook were active all seven days of a week on a mobile phone.

```python
con = connect_to_redshift()
ex = con.execute
from pandas import read_sql_query as qry
import pandas as pd
import numpy as np
from datetime import datetime
rc = np.random.choice

def timestamp(y0=2005,yf=2017):
  year = rc(range(y0,yf))
  month = rc(range(1,12))
  if month in [1,3,5,7,8,10,12]:
    dom = rc(range(1,32))
  elif month in [4,6,9,11]:
    dom = rc(range(1,31))
  else:
    dom = rc(range(1,29))
  hour = rc(range(0,24))
  min = rc(range(0,60))
  sec = rc(range(0,60))
  ts = datetime(year,month,dom,hour,min,sec)
  return ts
  
def user(n_users=337):
  return rc(range(n_users))

def device():
  return rc(['PC','PC','mobile', 'mobile','mobile','TV','TV','TV','TV','TV'])
  
tbl = pd.DataFrame(
  [[user(), timestamp(), device()] for i in range(10000)],
  columns=['userid', 'timestamp', 'device'])

tbl.to_sql('krbn_fb1', con=con, schema='krbn', index=False)  # might need to set a smaller chunksize!

# Python/Pandas Way
tbl['wkdy'] = [ts.weekday() for ts in tbl.timestamp]
tbl[tbl.device=='mobile']
```

https://pandas.pydata.org/pandas-docs/stable/groupby.html
