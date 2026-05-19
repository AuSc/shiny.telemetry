# Data storage class for `JSON` Log File

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to a `JSON` log file backend using a unified API for read/write
operations

## Super class

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\> `DataStorageLogFile`

## Active bindings

- `event_bucket`:

  string that identifies the file path to store user related and action
  data

## Methods

### Public methods

- [`DataStorageLogFile$new()`](#method-DataStorageLogFile-new)

- [`DataStorageLogFile$clone()`](#method-DataStorageLogFile-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStorageLogFile$new(log_file_path)

#### Arguments

- `log_file_path`:

  string with path to `JSON` log file user actions

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorageLogFile$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
log_file_path <- tempfile(fileext = ".txt")
data_storage <- DataStorageLogFile$new(log_file_path = log_file_path)

data_storage$insert("example", "test_event", "session1")
data_storage$insert("example", "input", "s1", list(id = "id"))
data_storage$insert("example", "input", "s1", list(id = "id2", value = 32))

data_storage$insert(
  "example", "test_event_3_days_ago", "session1",
  time = lubridate::as_datetime(lubridate::today() - 3)
)

data_storage$read_event_data()
#> # A tibble: 4 × 8
#>   app_name type      session time                id    value date       username
#>   <chr>    <chr>     <chr>   <dttm>              <chr> <chr> <date>     <chr>   
#> 1 example  test_eve… sessio… 2026-05-19 15:17:12 NA    NA    2026-05-19 NA      
#> 2 example  input     s1      2026-05-19 15:17:12 id    NA    2026-05-19 NA      
#> 3 example  input     s1      2026-05-19 15:17:12 id2   32    2026-05-19 NA      
#> 4 example  test_eve… sessio… 2026-05-16 00:00:00 NA    NA    2026-05-16 NA      
data_storage$read_event_data(Sys.Date() - 1, Sys.Date() + 1)
#> # A tibble: 3 × 8
#>   app_name type      session time                id    value date       username
#>   <chr>    <chr>     <chr>   <dttm>              <chr> <chr> <date>     <chr>   
#> 1 example  test_eve… sessio… 2026-05-19 15:17:12 NA    NA    2026-05-19 NA      
#> 2 example  input     s1      2026-05-19 15:17:12 id    NA    2026-05-19 NA      
#> 3 example  input     s1      2026-05-19 15:17:12 id2   32    2026-05-19 NA      

file.remove(log_file_path)
#> [1] TRUE
```
