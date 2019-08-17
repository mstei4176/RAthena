
# RAthena

The goal of the RAthena package is to provide a DBI-compliant interface
to Athena without the requirement of using odbc and jdbc drivers. This
will allow the connection to be athena to be straight forward and only
require the installation of python and the AWS SDK boto3.

With the development of AWS sagemaker RAthena will make the connection
to AWS Athena simpler.

## Installation:

``` r
remotes::install_bitbucket("shopdirect/rathena",
                           auth_user = "<bitbucket_username>",
                           password = "<bitbucket_password>")
```

## Usage

### Basic Usage

Connect to athena, and send a query and return results back to R.

``` r
library(DBI)

con <- dbConnect(RAthena::athena(),
                aws_access_key_id='YOUR_ACCESS_KEY_ID',
                aws_secret_access_key='YOUR_SECRET_ACCESS_KEY',
                s3_staging_dir='s3://YOUR_S3_BUCKET/path/to/',
                region_name='us-west-2')

res <- dbExecute(con, "SELECT * FROM one_row")
dbFetch(res)
dbClearResult(res)
```

To retrieve query in 1 step.

``` r
dbGetQuery(con, "SELECT * FROM one_row")
```

### Tidyverse Usage

``` r
library(DBI)
library(dplyr)

con <- dbConnect(RAthena::athena(),
                aws_access_key_id='YOUR_ACCESS_KEY_ID',
                aws_secret_access_key='YOUR_SECRET_ACCESS_KEY',
                s3_staging_dir='s3://YOUR_S3_BUCKET/path/to/',
                region_name='us-west-2')
tbl(con, sql("SELECT * FROM one_row"))
```
