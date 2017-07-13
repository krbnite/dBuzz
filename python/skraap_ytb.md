
http://docs.python-requests.org/en/master/user/quickstart/

## Clicking on JavaScript Buttons
I basically followed advice from this [StackOverflow page](https://stackoverflow.com/questions/8960288/get-page-generated-with-javascript-in-python/8960386#8960386)

I first tried the Chrome browser from selenium, but got the error message stating
that I must install the drivers.  Instead, I tried the Safari browser from selenium.
It actually worked for a second, but (1) I had to enter my password, which worked; and
(2) I had to enter some other password that I couldn't figure out.

Update: As interesting as this part of the project is, I was finally given access to
the table that just tells me which new videos the company has uploaded in the last
few days, along w/ their video IDs.  Given this, I can access the webpages directly
using requests...  That said, I'll likely need to return to this for the 2nd stage
of the project for clicking on the statistics button!


```python
# pip install: bs4, requests, selenium
# requests is great for just grabbing the HTML, but YT has a javascript
#   button that needs to be pressed to load more content...and for this we
#   need selenium
import bs4 # beautiful soup
import requests
import selenium

r = requests.get("https://www.youtube.com/watch?v=zh9NgGf3cxU")
# Or...
vidkey = {'v': 'zh9NgGf3cxU'}
r = requests.get("https://www.youtube.com/watch", params=vidkey)

# See it
r.text
# Or...
bsr = bs4.BeautifulSoup(r.text)
bsr.contents

# Probably will stick w/ pure requests for now

# See header info
r.headers
r.headers['content-type']

# Encoding
r.encoding
```

Find stuff
```python
tag_start = r.text.find('watch-view-count')
num_start = tag_start + r.text[tag_start:].find(">") + 1
num_end = num_start + r.text[num_start:].find('view') -1
num = int(''.join(r.text[num_start:num_end].split(',')))
```



## pandas
https://pandas.pydata.org/pandas-docs/stable/io.html#schema-support

```python
import pandas as pd

# A lot of useful stuff in v0.20+ (e.g., to_sql)
assert int(pd.__version[2:4]) >= 20, \
  'update pandas!'

# Use sqlalchemy to connect to redshift
from sqlalchemy import create_engine
con_str = 'postgresql://'+user+':'+pswd+'@'+host+':5439/'+db
con = create_engine(con_str)

# My pandas-to-redshift shorthands
qry = pd.read_sql_qry
tqry = pd.read_sql_table

# Read table from Redshift
myDf = qry("select * from mySchema.myTbl", con)
otherDf = tqry('otherTbl', con, schema=mySchema)

# Write a new table to Redshift
# -- the default is write the pd.DataFrame's index as its own column,
#    which might be useful sometimes, but I haven't found when
myDict = {'col1': col1, 'col2': col2}
myNewDf = pd.DataFrame(myDict)
myNewDf.to_sql('myNewTbl', con, schema=mySchema, index=False)

# Append data to an pre-existing table
#  -- if a table exists, the default is to fail
#  -- however, one can choose to overwrite it or append to it
similarDf = pd.DataFrame({'col1': c1, 'col2': c2})
myDf = myNewDf.append(similarDf)
myDf.to_sql('myTbl', con, schema=mySchema, index=False, if_exists='append')

```


## Using sqlalchemy to enhance pandas
https://pandas.pydata.org/pandas-docs/stable/io.html#schema-support

```python
import sqlalchemy as sa
from pandas import read_sql_query as qry

metadata = sa.MetaData()

yt_tbl = sa.Table(
  'most_recent_youtube_stats', metadata, 
  sa.Column('video_id', sa.String), 
  sa.Column('title', sa.String), 
  sa.Column('time_uploaded', sa.DateTime), 
  sa.Column('as_on_date', sa.Date))

# What's in it?
qry(sa.select([yt_tbl]), con)

q = sa.select([yt_tbl]).where(yt_tbl.c.time_uploaded >= tbl.c.as_on_date)
qry(q,con)
```


## Beautiful Soup

```python
import requests
import bs4 as bs
page = requests.get(url)
soup = bs.BeautifulSoup(page.text, 'lxml')  

# page in its ugly form
soup.text

# page in its beautiful form
soup.contents

# Find first div tag
soup.find('div')

# Find first div tag w/ id=ID
soup.find('div', id=ID)  # soup.find('div', {'id':ID})

# Find all top-level div tags
div = soup.find_all('div')

# Find all buttons w/ attribut attr==False
button = soup.find_all('button', {'attr':False})

# Find all images w/ alt=='pic' and width=='23'
#  -- note: the following two commands both work, however
#           the 2nd command is likely preferable b/c it is
#           specific and b/c the first way does not seem to work for 'class'
soup.find_all('img', alt='pic', width='23')
soup.find_all('img', {'alt':'pic','width':'23'})

```


## Selenium
Began learning how to use this, but now have better way.
