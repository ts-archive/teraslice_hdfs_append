# Description

Appends chunks of data to files in HDFS. To avoid concurrency issues the files will be given unique names associated with each worker.

# Expected Inputs

Array of chunked data requests as generated by `teraslice_file_chunker`.

# Output

Currently undefined.

# Parameters

| Name | Description | Default | Required |
| ---- | ----------- | ------- | -------- |
| connection | Name of the terafoundation HDFS connection to use | default | N |

# Job configuration example

Simple configuration example or examples as needed.

```
{
  "name": "Data Generator",
  "lifecycle": "persistent",
  "workers": 1,
  "operations": [
    {
      "_op": "elasticsearch_data_generator",
      "size": 5000
    },
    {
      "_op": "teraslice_file_chunker",
      "timeseries": "daily",
      "date_field": "created",
      "directory": "/testpath/test"
    },
    {
      "_op": "teraslice_hdfs_append"
    }
  ]
}
```

# Notes

This module is designed to be used in coordination with `teraslice_file_chunker` or a similar pre-processor that allocates the data into reasonable sized chunks to send to HDFS.
