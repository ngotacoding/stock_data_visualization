# IBM-Python-Project-for-DS

## Project Overview

Python is a major programming language in the Data Science Ecosystem. This project aims to evaluate the learner's understanding of the Python essentials especially in a Data Science oriented environment. 
- The project illustrates the process of data extraction using APIs and webscraping, and creating a [pandas dataframe](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) from the data.
- The project shows hands-on implementation of functions in data science projects, including a sample situation where functional programming is used in a data science plotting task. 
- The project introduces the [plotly](https://plotly.com/python/) library for data visualization. You learn to hasten the process of making graphs by writing reusable functions, and the process of making graphs for stock data visualization.
- The project illustrates the basics of getting finance market data using [yfinance](https://pypi.org/project/yfinance/). [yfinance](https://pypi.org/project/yfinance/) provides a means to access finance market data from [Yahoo Finance](https://finance.yahoo.com/) for analysis. 
- The project illustrates the basics of webscraping using [requests](https://requests.readthedocs.io/en/latest/) and [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).  

## Libraries and Tools used

The project uses [yfinance](https://pypi.org/project/yfinance/), [Requests](https://requests.readthedocs.io/en/latest/) and [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) for data extraction, [Pandas](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) for data cleaning, and [Plotly](https://plotly.com/python/) for data visualization. The lxml parser is used with [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).


### Installing the libraries

The libraries are installed using the `pip install` command. 

```bash
pip install pandas
pip install requests
pip install bs4
pip install yfinance
pip install plotly
pip install lxml
```

The specific version can be specified by adding `==<version_number>` as a suffix. Replace <version_number> with version number specified.


## The process

- Import the libraries; importing pandas as pd and yfinance as yf.
- The predefined `make_graph(stock_data, revenue_data, stock)` function makes 2 time-series plots. 
    - `stock_data` is a containing stock data and must contain Date and Close columns. 
    - `revenue_data` is a dataframe with revenue data and must contain Date and Revenue columns).
    - `stock` is the name of the stock whose stock and revenue data is presented in the 2 dataframes.

### Extracting stock data using yfinance

- Using the ticker symbol of the stock we want to extract, initialize a ticker object with the ticker symbol as the argument. Assign the object to a variable.
Example using Tesla Stock,

```python
tesla = yf.Ticker("TSLA")
```

- Use the `history(period)` funtion on the ticker object to extract historical stock information and save it in a dataframe. The period argument specifies the timeframe of the data. In this project, the maximum period was desired hence `period = 'max'`

```python
tesla_data = tesla.history(period = "max")
```

### Extracting stock data using requests and beautiful soup

To use requests, ensure you have the url of the data you want to obtain. Then run the following lines of code.
```python 
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, 'lxml')
tesla_revenue = pd.read_html(str(soup), match = "Tesla Quarterly Revenue", flavor = 'bs4')[0]
``` 
- `html_data = requests.get(url).text` retrieves the HTML contents of the webpage and assigns them to a variable html_data.

- `soup = BeautifulSoup(html_data, 'lxml')` parses the HTML data using Beautiful Soup. The lxml parser is used.
- The last line reads through the html markup using pandas and extracts tables that meet the match criteria. 
    - `flavor = bs4` specifies to use Beautiful soup as the parsing engine
    - `match` is the criterion selected tables must meet to be selected. In our case, tables called "Tesla Quarterly Revenue" are selected.
    - `)[0]` indexing specifies to select the first table of the tables selected. Indexing used is zero-indexing.
    
## About
This is a project on Data Visualization of stock data as part of the curriculum for [IBM python project for Data Science Course](https://www.coursera.org/learn/python-project-for-data-science?specialization=ibm-data-science) on [Coursera](https://www.coursera.org/).