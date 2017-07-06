
http://docs.python-requests.org/en/master/user/quickstart/

```python
import bs4 # beautiful soup
import requests

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
