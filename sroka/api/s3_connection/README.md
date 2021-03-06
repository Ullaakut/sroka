# s3 download data API

## Methods


### `s3_download_data(s3_filename, prefix=False, output_file='', sep=',')`


#### Arguments

* string `s3_filename` - pathway to file or prefix on s3 (obligatory)
* Bool `prefix` - if `s3_filename` should be treated as file path (`False`) or prefix (`True`) 
(default: `False`)
* string `output_file` - if `None` function will return pandas DataFrame, if filename - DataFrame will be
saved to defined file (default: `None`)
* string `sep` - what separator is used in (default: `,`)

#### Returns

* pandas DataFrame

## Usage
```python

from sroka.api.s3_connection.s3_connection_api import s3_download_data

df = s3_download_data('s3://bucket/folder/2019_01_01/part-111-111-111-111-111-111.csv',
   prefix=False)
   
df2 = s3_download_data('s3://bucket/folder/2019_01_01/', prefix=True, sep=';')

s3_download_data('s3://bucket/folder/2019_01_01/', output_file='./clicked.csv', prefix=True)

s3_download_data('s3://bucket/folder/2019_01_01/part-111-111-111-111-111-111.csv', 
   output_file='./clicked_1.csv')
```