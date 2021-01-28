# Google-Ads-Keyword-Research
Google Ads Keyword Research

```python
from IPython.display import display, HTML
import pandas as pd
import json 
import matplotlib.pyplot as plt

from pytrends.request import TrendReq
def getTrends(term, res):
    #Connect to google trends object
    pytrend = TrendReq()
    
    #Search Terms
    pytrend.build_payload(kw_list = term) # Interest by Region
    
    #build Region Data sorted by intrest and term order
    df = pytrend.interest_by_region()
    df = df.sort_values(by=term, ascending=False).head(res)
    
    #plot Geographic data
    df.reset_index().plot(x="geoName", y=term, figsize=(10, 6), kind ='bar',title="Amount of Interest: 0-100")
    plt.show()
    
    #table of Geo data
    display(HTML(df.to_html()))
    
    #get Intrest over time
    df = pytrend.interest_over_time()
    
    #plot over Times data
    df.reset_index().plot(x="date", y=term, figsize=(10, 6), kind ='line',title="Amount of Interest over time")
    plt.show()
    
    #get related queries
    dc = pytrend.related_queries()
    
    #print tables for each search term. 
    for item in dc:
        print("Related Queries for: " + item)    
        display(HTML(pd.DataFrame.from_dict(dc[item]["top"]).to_html()))
        
#terms = ["list", "of", "terms", "max of 4"]
#getTrends(terms, INT size of chart and table)  
```
