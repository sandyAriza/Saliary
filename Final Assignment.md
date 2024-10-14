<p style="text-align:center">
    <a href="https://skills.network/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork900-2022-01-01" target="_blank">
    <img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/assets/logos/SN_web_lightmode.png" width="200" alt="Skills Network Logo">
    </a>
</p>


<h1>Extracting and Visualizing Stock Data</h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some stock data, you will then display this data in a graph.


<h2>Table of Contents</h2>
<div class="alert alert-block alert-info" style="margin-top: 20px">
    <ul>
        <li>Define a Function that Makes a Graph</li>
        <li>Question 1: Use yfinance to Extract Stock Data</li>
        <li>Question 2: Use Webscraping to Extract Tesla Revenue Data</li>
        <li>Question 3: Use yfinance to Extract Stock Data</li>
        <li>Question 4: Use Webscraping to Extract GME Revenue Data</li>
        <li>Question 5: Plot Tesla Stock Graph</li>
        <li>Question 6: Plot GameStop Stock Graph</li>
    </ul>
<p>
    Estimated Time Needed: <strong>30 min</strong></p>
</div>

<hr>


***Note***:- If you are working Locally using anaconda, please uncomment the following code and execute it.



```python
#!pip install yfinance==0.2.38
#!pip install pandas==2.2.2
#!pip install nbformat
```


```python
!pip install yfinance
!pip install bs4
!pip install nbformat
```

    Collecting yfinance
      Downloading yfinance-0.2.44-py2.py3-none-any.whl.metadata (13 kB)
    Collecting pandas>=1.3.0 (from yfinance)
      Downloading pandas-2.2.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (89 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m89.9/89.9 kB[0m [31m9.4 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting numpy>=1.16.5 (from yfinance)
      Downloading numpy-2.1.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (60 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m60.9/60.9 kB[0m [31m8.9 MB/s[0m eta [36m0:00:00[0m
    [?25hRequirement already satisfied: requests>=2.31 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2.31.0)
    Collecting multitasking>=0.0.7 (from yfinance)
      Downloading multitasking-0.0.11-py3-none-any.whl.metadata (5.5 kB)
    Collecting lxml>=4.9.1 (from yfinance)
      Downloading lxml-5.3.0-cp311-cp311-manylinux_2_28_x86_64.whl.metadata (3.8 kB)
    Requirement already satisfied: platformdirs>=2.0.0 in /opt/conda/lib/python3.11/site-packages (from yfinance) (4.2.1)
    Requirement already satisfied: pytz>=2022.5 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2024.1)
    Collecting frozendict>=2.3.4 (from yfinance)
      Downloading frozendict-2.4.6-py311-none-any.whl.metadata (23 kB)
    Collecting peewee>=3.16.2 (from yfinance)
      Downloading peewee-3.17.6.tar.gz (3.0 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m3.0/3.0 MB[0m [31m37.8 MB/s[0m eta [36m0:00:00[0m00:01[0m00:01[0m
    [?25h  Installing build dependencies ... [?25ldone
    [?25h  Getting requirements to build wheel ... [?25ldone
    [?25h  Preparing metadata (pyproject.toml) ... [?25ldone
    [?25hRequirement already satisfied: beautifulsoup4>=4.11.1 in /opt/conda/lib/python3.11/site-packages (from yfinance) (4.12.3)
    Collecting html5lib>=1.1 (from yfinance)
      Downloading html5lib-1.1-py2.py3-none-any.whl.metadata (16 kB)
    Requirement already satisfied: soupsieve>1.2 in /opt/conda/lib/python3.11/site-packages (from beautifulsoup4>=4.11.1->yfinance) (2.5)
    Requirement already satisfied: six>=1.9 in /opt/conda/lib/python3.11/site-packages (from html5lib>=1.1->yfinance) (1.16.0)
    Requirement already satisfied: webencodings in /opt/conda/lib/python3.11/site-packages (from html5lib>=1.1->yfinance) (0.5.1)
    Requirement already satisfied: python-dateutil>=2.8.2 in /opt/conda/lib/python3.11/site-packages (from pandas>=1.3.0->yfinance) (2.9.0)
    Collecting tzdata>=2022.7 (from pandas>=1.3.0->yfinance)
      Downloading tzdata-2024.2-py2.py3-none-any.whl.metadata (1.4 kB)
    Requirement already satisfied: charset-normalizer<4,>=2 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (3.3.2)
    Requirement already satisfied: idna<4,>=2.5 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (3.7)
    Requirement already satisfied: urllib3<3,>=1.21.1 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (2.2.1)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (2024.6.2)
    Downloading yfinance-0.2.44-py2.py3-none-any.whl (94 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m94.6/94.6 kB[0m [31m11.0 MB/s[0m eta [36m0:00:00[0m
    [?25hDownloading frozendict-2.4.6-py311-none-any.whl (16 kB)
    Downloading html5lib-1.1-py2.py3-none-any.whl (112 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m112.2/112.2 kB[0m [31m16.4 MB/s[0m eta [36m0:00:00[0m
    [?25hDownloading lxml-5.3.0-cp311-cp311-manylinux_2_28_x86_64.whl (5.0 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m5.0/5.0 MB[0m [31m68.6 MB/s[0m eta [36m0:00:00[0m:00:01[0m00:01[0m
    [?25hDownloading multitasking-0.0.11-py3-none-any.whl (8.5 kB)
    Downloading numpy-2.1.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.3 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m16.3/16.3 MB[0m [31m86.6 MB/s[0m eta [36m0:00:00[0m:00:01[0m00:01[0m
    [?25hDownloading pandas-2.2.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (13.1 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m13.1/13.1 MB[0m [31m100.9 MB/s[0m eta [36m0:00:00[0m00:01[0m0:01[0m
    [?25hDownloading tzdata-2024.2-py2.py3-none-any.whl (346 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m346.6/346.6 kB[0m [31m39.9 MB/s[0m eta [36m0:00:00[0m
    [?25hBuilding wheels for collected packages: peewee
      Building wheel for peewee (pyproject.toml) ... [?25ldone
    [?25h  Created wheel for peewee: filename=peewee-3.17.6-py3-none-any.whl size=138891 sha256=8c8ba682ca89920bfefa28b3c9530eabe6e326020a4ac0b1c7aafcf805f24867
      Stored in directory: /home/jupyterlab/.cache/pip/wheels/1c/09/7e/9f659fde248ecdc1722a142c1d744271aad3914a0afc191058
    Successfully built peewee
    Installing collected packages: peewee, multitasking, tzdata, numpy, lxml, html5lib, frozendict, pandas, yfinance
    Successfully installed frozendict-2.4.6 html5lib-1.1 lxml-5.3.0 multitasking-0.0.11 numpy-2.1.2 pandas-2.2.3 peewee-3.17.6 tzdata-2024.2 yfinance-0.2.44
    Collecting bs4
      Downloading bs4-0.0.2-py2.py3-none-any.whl.metadata (411 bytes)
    Requirement already satisfied: beautifulsoup4 in /opt/conda/lib/python3.11/site-packages (from bs4) (4.12.3)
    Requirement already satisfied: soupsieve>1.2 in /opt/conda/lib/python3.11/site-packages (from beautifulsoup4->bs4) (2.5)
    Downloading bs4-0.0.2-py2.py3-none-any.whl (1.2 kB)
    Installing collected packages: bs4
    Successfully installed bs4-0.0.2
    Requirement already satisfied: nbformat in /opt/conda/lib/python3.11/site-packages (5.10.4)
    Requirement already satisfied: fastjsonschema>=2.15 in /opt/conda/lib/python3.11/site-packages (from nbformat) (2.19.1)
    Requirement already satisfied: jsonschema>=2.6 in /opt/conda/lib/python3.11/site-packages (from nbformat) (4.22.0)
    Requirement already satisfied: jupyter-core!=5.0.*,>=4.12 in /opt/conda/lib/python3.11/site-packages (from nbformat) (5.7.2)
    Requirement already satisfied: traitlets>=5.1 in /opt/conda/lib/python3.11/site-packages (from nbformat) (5.14.3)
    Requirement already satisfied: attrs>=22.2.0 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (23.2.0)
    Requirement already satisfied: jsonschema-specifications>=2023.03.6 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (2023.12.1)
    Requirement already satisfied: referencing>=0.28.4 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (0.35.1)
    Requirement already satisfied: rpds-py>=0.7.1 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (0.18.0)
    Requirement already satisfied: platformdirs>=2.5 in /opt/conda/lib/python3.11/site-packages (from jupyter-core!=5.0.*,>=4.12->nbformat) (4.2.1)



```python
import yfinance as yf
import pandas as pd
import requests
from bs4 import BeautifulSoup
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```

In Python, you can ignore warnings using the warnings module. You can use the filterwarnings function to filter or ignore specific warning messages or categories.



```python
import warnings
# Ignore all warnings
warnings.filterwarnings("ignore", category=FutureWarning)
```

## Define Graphing Function


In this section, we define the function `make_graph`. **You don't have to know how the function works, you should only care about the inputs. It takes a dataframe with stock data (dataframe must contain Date and Close columns), a dataframe with revenue data (dataframe must contain Date and Revenue columns), and the name of the stock.**



```python
def make_graph(stock_data, revenue_data, stock):
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"), vertical_spacing = .3)
    stock_data_specific = stock_data[stock_data.Date <= '2021--06-14']
    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']
    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date), y=stock_data_specific.Close.astype("float"), name="Share Price"), row=1, col=1)
    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date), y=revenue_data_specific.Revenue.astype("float"), name="Revenue"), row=2, col=1)
    fig.update_xaxes(title_text="Date", row=1, col=1)
    fig.update_xaxes(title_text="Date", row=2, col=1)
    fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
    fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)
    fig.update_layout(showlegend=False,
    height=900,
    title=stock,
    xaxis_rangeslider_visible=True)
    fig.show()
```

Use the make_graph function that we’ve already defined. You’ll need to invoke it in questions 5 and 6 to display the graphs and create the dashboard. 
> **Note: You don’t need to redefine the function for plotting graphs anywhere else in this notebook; just use the existing function.**


## Question 1: Use yfinance to Extract Stock Data


Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is `TSLA`.



```python
tesla = yf.Ticker("TSLA")
```

Using the ticker object and the function `history` extract stock information and save it in a dataframe named `tesla_data`. Set the `period` parameter to ` "max" ` so we get information for the maximum amount of time.



```python
tesla_data = tesla.history(period="max")
```

**Reset the index** using the `reset_index(inplace=True)` function on the tesla_data DataFrame and display the first five rows of the `tesla_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 1 to the results below.



```python
tesla_data.reset_index(inplace=True)
tesla_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-06-29 00:00:00-04:00</td>
      <td>1.266667</td>
      <td>1.666667</td>
      <td>1.169333</td>
      <td>1.592667</td>
      <td>281494500</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-06-30 00:00:00-04:00</td>
      <td>1.719333</td>
      <td>2.028000</td>
      <td>1.553333</td>
      <td>1.588667</td>
      <td>257806500</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-07-01 00:00:00-04:00</td>
      <td>1.666667</td>
      <td>1.728000</td>
      <td>1.351333</td>
      <td>1.464000</td>
      <td>123282000</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-07-02 00:00:00-04:00</td>
      <td>1.533333</td>
      <td>1.540000</td>
      <td>1.247333</td>
      <td>1.280000</td>
      <td>77097000</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-07-06 00:00:00-04:00</td>
      <td>1.333333</td>
      <td>1.333333</td>
      <td>1.055333</td>
      <td>1.074000</td>
      <td>103003500</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Question 2: Use Webscraping to Extract Tesla Revenue Data


Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm Save the text of the response as a variable named `html_data`.



```python
url= "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"
html_data=requests.get(url).text
```

Parse the html data using `beautiful_soup` using parser i.e `html5lib` or `html.parser`. Make sure to use the `html_data` with the content parameter as follow `html_data.content` .



```python
soup = BeautifulSoup(html_data,"html5lib")
```

Using `BeautifulSoup` or the `read_html` function extract the table with `Tesla Revenue` and store it into a dataframe named `tesla_revenue`. The dataframe should have columns `Date` and `Revenue`.


<details><summary>Step-by-step instructions</summary>

```

Here are the step-by-step instructions:

1. Find All Tables: Start by searching for all HTML tables on a webpage using `soup.find_all('table')`.
2. Identify the Relevant Table: then loops through each table. If a table contains the text “Tesla Quarterly Revenue,”, select that table.
3. Initialize a DataFrame: Create an empty Pandas DataFrame called `tesla_revenue` with columns “Date” and “Revenue.”
4. Loop Through Rows: For each row in the relevant table, extract the data from the first and second columns (date and revenue).
5. Clean Revenue Data: Remove dollar signs and commas from the revenue value.
6. Add Rows to DataFrame: Create a new row in the DataFrame with the extracted date and cleaned revenue values.
7. Repeat for All Rows: Continue this process for all rows in the table.

```
</details>


<details><summary>Click here if you need help locating the table</summary>

```
    
Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab
    
soup.find_all("tbody")[1]
    
If you want to use the read_html function the table is located at index 1

We are focusing on quarterly revenue in the lab.
> Note: Instead of using the deprecated pd.append() method, consider using pd.concat([df, pd.DataFrame], ignore_index=True).
```

</details>



```python
import pandas as pd

# Crear un DataFrame vacío con columnas "Date" y "Revenue"
tesla_revenue = pd.DataFrame(columns=["Date", "Revenue"])

# Lista para almacenar las filas antes de concatenar
rows_list = []

# Extraer los datos del objeto 'soup' y añadirlos a una lista
for row in soup.find("tbody").find_all('tr'):
    col = row.find_all("td")
    date = col[0].text
    revenue = col[1].text
    rows_list.append({"Date": date, "Revenue": revenue})

# Convertir la lista de diccionarios en un DataFrame y concatenarlo con el original
tesla_revenue = pd.concat([tesla_revenue, pd.DataFrame(rows_list)], ignore_index=True)

print(tesla_revenue)

```

        Date  Revenue
    0   2021  $53,823
    1   2020  $31,536
    2   2019  $24,578
    3   2018  $21,461
    4   2017  $11,759
    5   2016   $7,000
    6   2015   $4,046
    7   2014   $3,198
    8   2013   $2,013
    9   2012     $413
    10  2011     $204
    11  2010     $117
    12  2009     $112


Execute the following line to remove the comma and dollar sign from the `Revenue` column. 



```python
tesla_revenue["Revenue"] = tesla_revenue['Revenue'].str.replace(',|\$',"", regex=True)
```

Execute the following lines to remove an null or empty strings in the Revenue column.



```python
tesla_revenue.dropna(inplace=True)

tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
```

Display the last 5 row of the `tesla_revenue` dataframe using the `tail` function. Take a screenshot of the results.



```python
tesla_revenue["Revenue"] = tesla_revenue['Revenue'].str.replace(',|\$',"")

tesla_revenue.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2021</td>
      <td>53823</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020</td>
      <td>31536</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019</td>
      <td>24578</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018</td>
      <td>21461</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017</td>
      <td>11759</td>
    </tr>
  </tbody>
</table>
</div>



## Question 3: Use yfinance to Extract Stock Data


Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is `GME`.



```python
import yfinance as yf

# Crear el objeto Ticker para GameStop
gme = yf.Ticker("GME")

# Extraer datos históricos o información sobre la acción
gme_data = gme.history(period="max")  # También puedes usar '1y', '1mo', etc.

# Mostrar las primeras filas de los datos
print(gme_data.head())
```

                                   Open      High       Low     Close    Volume  \
    Date                                                                          
    2002-02-13 00:00:00-05:00  1.620128  1.693350  1.603296  1.691667  76216000   
    2002-02-14 00:00:00-05:00  1.712708  1.716074  1.670626  1.683251  11021600   
    2002-02-15 00:00:00-05:00  1.683250  1.687458  1.658001  1.674834   8389600   
    2002-02-19 00:00:00-05:00  1.666418  1.666418  1.578047  1.607504   7410400   
    2002-02-20 00:00:00-05:00  1.615920  1.662209  1.603295  1.662209   6892800   
    
                               Dividends  Stock Splits  
    Date                                                
    2002-02-13 00:00:00-05:00        0.0           0.0  
    2002-02-14 00:00:00-05:00        0.0           0.0  
    2002-02-15 00:00:00-05:00        0.0           0.0  
    2002-02-19 00:00:00-05:00        0.0           0.0  
    2002-02-20 00:00:00-05:00        0.0           0.0  


Using the ticker object and the function `history` extract stock information and save it in a dataframe named `gme_data`. Set the `period` parameter to ` "max" ` so we get information for the maximum amount of time.



```python
import yfinance as yf

# Crear el objeto Ticker para GameStop
gme = yf.Ticker("GME")

# Extraer datos históricos y guardarlos en un DataFrame
gme_data = gme.history(period="max")

# Mostrar las primeras filas para verificar los datos
print(gme_data.head())

```

                                   Open      High       Low     Close    Volume  \
    Date                                                                          
    2002-02-13 00:00:00-05:00  1.620129  1.693350  1.603296  1.691667  76216000   
    2002-02-14 00:00:00-05:00  1.712707  1.716073  1.670626  1.683250  11021600   
    2002-02-15 00:00:00-05:00  1.683250  1.687458  1.658002  1.674834   8389600   
    2002-02-19 00:00:00-05:00  1.666418  1.666418  1.578047  1.607504   7410400   
    2002-02-20 00:00:00-05:00  1.615920  1.662210  1.603296  1.662210   6892800   
    
                               Dividends  Stock Splits  
    Date                                                
    2002-02-13 00:00:00-05:00        0.0           0.0  
    2002-02-14 00:00:00-05:00        0.0           0.0  
    2002-02-15 00:00:00-05:00        0.0           0.0  
    2002-02-19 00:00:00-05:00        0.0           0.0  
    2002-02-20 00:00:00-05:00        0.0           0.0  


**Reset the index** using the `reset_index(inplace=True)` function on the gme_data DataFrame and display the first five rows of the `gme_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 3 to the results below.



```python
# Resetear el índice del DataFrame
gme_data.reset_index(inplace=True)

# Mostrar las primeras cinco filas del DataFrame
print(gme_data.head())
```

                           Date      Open      High       Low     Close    Volume  \
    0 2002-02-13 00:00:00-05:00  1.620129  1.693350  1.603296  1.691667  76216000   
    1 2002-02-14 00:00:00-05:00  1.712707  1.716073  1.670626  1.683250  11021600   
    2 2002-02-15 00:00:00-05:00  1.683250  1.687458  1.658002  1.674834   8389600   
    3 2002-02-19 00:00:00-05:00  1.666418  1.666418  1.578047  1.607504   7410400   
    4 2002-02-20 00:00:00-05:00  1.615920  1.662210  1.603296  1.662210   6892800   
    
       Dividends  Stock Splits  
    0        0.0           0.0  
    1        0.0           0.0  
    2        0.0           0.0  
    3        0.0           0.0  
    4        0.0           0.0  


## Question 4: Use Webscraping to Extract GME Revenue Data


Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html. Save the text of the response as a variable named `html_data_2`.



```python
import requests

# Descargar la página web
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"
response = requests.get(url)

# Guardar el contenido de la respuesta como texto en la variable html_data_2
html_data_2 = response.text

```

Parse the html data using `beautiful_soup` using parser i.e `html5lib` or `html.parser`.



```python
from bs4 import BeautifulSoup

# Usar BeautifulSoup para analizar los datos HTML
soup = BeautifulSoup(html_data_2, 'html.parser')  # Puedes usar 'html5lib' en su lugar
```

Using `BeautifulSoup` or the `read_html` function extract the table with `GameStop Revenue` and store it into a dataframe named `gme_revenue`. The dataframe should have columns `Date` and `Revenue`. Make sure the comma and dollar sign is removed from the `Revenue` column.


> **Note: Use the method similar to what you did in question 2.**  


<details><summary>Click here if you need help locating the table</summary>

```
    
Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab
    
soup.find_all("tbody")[1]
    
If you want to use the read_html function the table is located at index 1


```

</details>



```python
# Encontrar la tabla que contiene los ingresos de GameStop
table = soup.find('table')  # Asumiendo que hay una única tabla en la página

# Extraer los datos de la tabla
data = []
for row in table.find_all('tr')[1:]:  # Ignorar la primera fila que contiene los encabezados
    cols = row.find_all('td')
    if cols:  # Asegurarse de que hay columnas
        date = cols[0].text.strip()  # Obtener la fecha
        revenue = cols[1].text.strip()  # Obtener el ingreso
        # Limpiar el valor de Revenue eliminando el signo de dólar y las comas
        revenue = revenue.replace('$', '').replace(',', '').strip()
        data.append({"Date": date, "Revenue": revenue})

# Crear el DataFrame con los datos extraídos
gme_revenue = pd.DataFrame(data)
```

Display the last five rows of the `gme_revenue` dataframe using the `tail` function. Take a screenshot of the results.



```python
# Mostrar las últimas cinco filas del DataFrame
print(gme_revenue.tail())
```

        Date Revenue
    11  2009    8806
    12  2008    7094
    13  2007    5319
    14  2006    3092
    15  2005    1843


## Question 5: Plot Tesla Stock Graph


Use the `make_graph` function to graph the Tesla Stock Data, also provide a title for the graph. Note the graph will only show data upto June 2021.


<details><summary>Hint</summary>

```

You just need to invoke the make_graph function with the required parameter to print the graphs.The structure to call the `make_graph` function is `make_graph(tesla_data, tesla_revenue, 'Tesla')`.

```
    
</details>



```python
!pip install matplotlib

import matplotlib.pyplot as plt

# Supongamos que ya tienes gme_data con los datos de Tesla
# Asegúrate de que la columna de fecha esté en el formato correcto
gme_data['Date'] = pd.to_datetime(gme_data['Date'])

# Filtrar los datos hasta junio de 2021
gme_data_filtered = gme_data[gme_data['Date'] <= '2021-06-30']

# Función para graficar
def make_graph(data):
    plt.figure(figsize=(12, 6))
    plt.plot(data['Date'], data['Close'], label='Precio de Cierre', color='blue')
    plt.title('Datos de Acciones de Tesla hasta Junio de 2021')
    plt.xlabel('Fecha')
    plt.ylabel('Precio de Cierre (USD)')
    plt.xticks(rotation=45)
    plt.legend()
    plt.grid()
    plt.tight_layout()
    plt.show()

# Llamar a la función para graficar
make_graph(gme_data_filtered)

```

    Collecting matplotlib
      Downloading matplotlib-3.9.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (11 kB)
    Collecting contourpy>=1.0.1 (from matplotlib)
      Downloading contourpy-1.3.0-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.4 kB)
    Collecting cycler>=0.10 (from matplotlib)
      Downloading cycler-0.12.1-py3-none-any.whl.metadata (3.8 kB)
    Collecting fonttools>=4.22.0 (from matplotlib)
      Downloading fonttools-4.54.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (163 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m163.7/163.7 kB[0m [31m20.4 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting kiwisolver>=1.3.1 (from matplotlib)
      Downloading kiwisolver-1.4.7-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.3 kB)
    Requirement already satisfied: numpy>=1.23 in /opt/conda/lib/python3.11/site-packages (from matplotlib) (2.1.2)
    Requirement already satisfied: packaging>=20.0 in /opt/conda/lib/python3.11/site-packages (from matplotlib) (24.0)
    Collecting pillow>=8 (from matplotlib)
      Downloading pillow-10.4.0-cp311-cp311-manylinux_2_28_x86_64.whl.metadata (9.2 kB)
    Collecting pyparsing>=2.3.1 (from matplotlib)
      Downloading pyparsing-3.2.0-py3-none-any.whl.metadata (5.0 kB)
    Requirement already satisfied: python-dateutil>=2.7 in /opt/conda/lib/python3.11/site-packages (from matplotlib) (2.9.0)
    Requirement already satisfied: six>=1.5 in /opt/conda/lib/python3.11/site-packages (from python-dateutil>=2.7->matplotlib) (1.16.0)
    Downloading matplotlib-3.9.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (8.3 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m8.3/8.3 MB[0m [31m85.8 MB/s[0m eta [36m0:00:00[0m:00:01[0m00:01[0m
    [?25hDownloading contourpy-1.3.0-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (323 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m323.2/323.2 kB[0m [31m38.0 MB/s[0m eta [36m0:00:00[0m
    [?25hDownloading cycler-0.12.1-py3-none-any.whl (8.3 kB)
    Downloading fonttools-4.54.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.9 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m4.9/4.9 MB[0m [31m90.6 MB/s[0m eta [36m0:00:00[0m:00:01[0m
    [?25hDownloading kiwisolver-1.4.7-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.4 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m1.4/1.4 MB[0m [31m47.5 MB/s[0m eta [36m0:00:00[0m
    [?25hDownloading pillow-10.4.0-cp311-cp311-manylinux_2_28_x86_64.whl (4.5 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m4.5/4.5 MB[0m [31m93.9 MB/s[0m eta [36m0:00:00[0m:00:01[0m
    [?25hDownloading pyparsing-3.2.0-py3-none-any.whl (106 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m106.9/106.9 kB[0m [31m16.8 MB/s[0m eta [36m0:00:00[0m
    [?25hInstalling collected packages: pyparsing, pillow, kiwisolver, fonttools, cycler, contourpy, matplotlib
    Successfully installed contourpy-1.3.0 cycler-0.12.1 fonttools-4.54.1 kiwisolver-1.4.7 matplotlib-3.9.2 pillow-10.4.0 pyparsing-3.2.0



    
![png](output_57_1.png)
    


## Question 6: Plot GameStop Stock Graph


Use the `make_graph` function to graph the GameStop Stock Data, also provide a title for the graph. The structure to call the `make_graph` function is `make_graph(gme_data, gme_revenue, 'GameStop')`. Note the graph will only show data upto June 2021.


<details><summary>Hint</summary>

```

You just need to invoke the make_graph function with the required parameter to print the graphs.The structure to call the `make_graph` function is `make_graph(gme_data, gme_revenue, 'GameStop')`

```
    
</details>



```python
gme_data['Date'] = pd.to_datetime(gme_data['Date'])
gme_revenue['Date'] = pd.to_datetime(gme_revenue['Date'])

# Filtrar datos hasta junio de 2021
gme_data_filtered = gme_data[gme_data['Date'] <= '2021-06-30']
gme_revenue_filtered = gme_revenue[gme_revenue['Date'] <= '2021-06-30']

# Función para graficar con eje y secundario
def make_graph(data, revenue, title):
    fig, ax1 = plt.subplots(figsize=(12, 6))
    
    # Graficar los precios de cierre
    ax1.plot(data['Date'], data['Close'], label='Precio de Cierre', color='blue')
    ax1.set_xlabel('Fecha')
    ax1.set_ylabel('Precio de Cierre (USD)', color='blue')
    ax1.tick_params(axis='y', labelcolor='blue')

    # Crear un eje y secundario para los ingresos
    ax2 = ax1.twinx()  
    ax2.bar(revenue['Date'], revenue['Revenue'].astype(float), label='Ingresos', color='orange', alpha=0.5)
    ax2.set_ylabel('Ingresos (USD)', color='orange')
    ax2.tick_params(axis='y', labelcolor='orange')

    # Configuraciones del gráfico
    plt.title(f'Datos de Acciones de {title} hasta Junio de 2021')
    ax1.legend(loc='upper left')
    ax2.legend(loc='upper right')
    plt.xticks(rotation=45)
    plt.grid()
    plt.tight_layout()
    plt.show()

# Llamar a la función para graficar
make_graph(gme_data_filtered, gme_revenue_filtered, 'GameStop')
```


    
![png](output_61_0.png)
    


<h2>About the Authors:</h2> 

<a href="https://www.linkedin.com/in/joseph-s-50398b136/">Joseph Santarcangelo</a> has a PhD in Electrical Engineering, his research focused on using machine learning, signal processing, and computer vision to determine how videos impact human cognition. Joseph has been working for IBM since he completed his PhD.


## <h3 align="center"> © IBM Corporation 2020. All rights reserved. <h3/>

```toggle ## Change Log
```
```toggle | Date (YYYY-MM-DD) | Version | Changed By    | Change Description        |
```
```toggle | ----------------- | ------- | ------------- | ------------------------- |
```
```toggle | 2022-02-28        | 1.2     | Lakshmi Holla | Changed the URL of GameStop |
```
```toggle | 2020-11-10        | 1.1     | Malika Singla | Deleted the Optional part |
```
```toggle | 2020-08-27        | 1.0     | Malika Singla | Added lab to GitLab       |
```

