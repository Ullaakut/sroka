# GA API

## Methods

### `ga_request(input_dict, print_sample_size, sampling_level)`

#### Arguments

* dict `input_dict` - required, the dictionary that contains the request to run on the Google Analytics API
* boolean `print_sample_size` - optional, will print the percentage of data that was used to calculate results. Default value is `False`.
* string `sampling_level` - optional, specifies the precision of your query. Available values are: `DEFAULT`, `FASTER`, 
or `HIGHER_PRECISION`. The default value is `HIGHER_PRECISION`. 

#### Returns

* A [`DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) containing the query results.

## Example usage

```python
from sroka.api.ga.ga import ga_request

request = {
"ids" : "ga:12345678",
"start_date" : "2018-05-01",
"end_date" : "2018-05-07",
"metrics" : "ga:pageviews,ga:sessions,ga:bounceRate,ga:avgTimeOnPage,ga:avgPageLoadTime",
"filters" : "ga:deviceCategory=~desktop,ga:deviceCategory=~tablet",
"segment" : "",
"dimensions" : "ga:day"
}

df_ga = ga_request(request, print_sample_size=True, sampling_level='FASTER')
```
