# Athena API

## Methods

### `query_athena(input_query, filename)`

#### Arguments

* string `input_query` - query to run
* string `filename` - path to the file in which to store the results (optional, if `filename=None`, results are returned as a [`pandas`](https://pandas.pydata.org/pandas-docs/stable/) [`DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html))

#### Returns

* A [`DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) containing the query results or `None` if the data was saved to a file.

#### Usage

```python
from sroka.api.athena.athena_api import query_athena

## Results saved to the file `results.csv`.
query_athena("""
    SELECT * FROM db.table
    WHERE year='2018' and month='10' and day='07'
    LIMIT 10
""", 'results.csv')

## Results saved to the variable `dataframe`, as a pandas.DataFrame.
dataframe = query_athena("""
    SELECT * FROM db.table
    WHERE year='2018' and month='10' and day='07'
    LIMIT 10
""")
```

### `done_athena(query_id, filename)`

#### Arguments

* string `query_id` - ID of the previous query from which to get the data
* string `filename` - path to the file in which to store the results (optional, if `filename=None`, results are returned as a [`pandas`](https://pandas.pydata.org/pandas-docs/stable/) [`DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html))

#### Returns

* A [`DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) containing the query results or `None` if the data was saved to a file.

#### Usage

```python
from sroka.api.athena.athena_api import done_athena

## Results saved to the file `results.csv`.
done_athena('1111111-222-3333-44444-55555555', 'results.csv')

## Results saved to the variable `dataframe`, as a pandas.DataFrame.
done_athena('1111111-222-3333-44444-55555555')
```

