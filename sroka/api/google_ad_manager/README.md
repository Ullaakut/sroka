# Google Ad Manager API

## Methods

### `get_data_from_admanager(query, dimensions, columns, start_date, stop_date, custom_field_id, network_code)`

#### Arguments

* string `query` - required, the query to run on Google Ad Manager
* list `dimensions` - required
* list `columns` - required, the list of all v to fetch
* dict `start_date` - required, a dictionary that contains the year, month and day from which to fetch data
* dict `stop_date` - required, a dictionary that contains the year, month and day until which to fetch data
* list `custom_field_id` -  list of ints, default is an empty list, not required. **Warning: In order to use `custom_field_id`, a corresponding dimension is needed**
* int `network_code` - the default value taken from the `config.ini` file. If the same service account has access to more than one network, the default value can be overwritten with this argument.

What is the purpose of the `custom_field_id`?

* Custom fields are additional fields that can be applied to orders, line items, and creatives. These fields can be used to organize objects in reports. Fields can be applied to particular objects by setting a value for them.
* In order to find the ID of a custom field, go to `GAM Dashboard` -> `Admin` -> `Global settings` -> `Custom Fields` -> `Choose Custom Field` and its ID can then be found in URL.

#### Returns

* A [`DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) containing the query results.

## Example usage

```python
from sroka.api.google_ad_manager.gam_api import get_data_from_admanager

start_day = '01'
end_day='01'
start_month = '08'
end_month = '08'
year = '2017'

# Data from GAM - orders
query = "WHERE CUSTOM_TARGETING_VALUE_ID=12345"
dimensions = ['DATE', 'LINE_ITEM_NAME']
custom_field_id = [54321]
columns = ['TOTAL_INVENTORY_LEVEL_IMPRESSIONS', 
           'TOTAL_ACTIVE_VIEW_MEASURABLE_IMPRESSIONS',
           'TOTAL_ACTIVE_VIEW_VIEWABLE_IMPRESSIONS']
start_date = {'year': year,
              'month': start_month,
              'day': start_day}
stop_date = {'year': year,
             'month': end_month,
             'day': end_day}

data = get_data_from_admanager(query, dimensions, columns, start_date, stop_date, custom_field_id, network_code=1234)
```
