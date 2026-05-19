# Data storage class with SQLite provider

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to SQLite backend using a unified API for read/write operations

## Super classes

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\>
[`shiny.telemetry::DataStorageSQLFamily`](https://appsilon.github.io/shiny.telemetry/reference/DataStorageSQLFamily.md)
-\> `DataStorageSQLite`

## Methods

### Public methods

- [`DataStorageSQLite$new()`](#method-DataStorageSQLite-new)

- [`DataStorageSQLite$clone()`](#method-DataStorageSQLite-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStorageSQLite$new(db_path = "user_stats.sqlite")

#### Arguments

- `db_path`:

  string with path to `SQLite` file.

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorageSQLite$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
db_path <- tempfile(fileext = ".sqlite")
data_storage <- DataStorageSQLite$new(db_path = db_path)

data_storage$insert("example", "test_event", "session1")
data_storage$insert("example", "input", "s1", list(id = "id1"))
data_storage$insert("example", "input", "s1", list(id = "id2", value = 32))

data_storage$insert(
  "example", "test_event_3_days_ago", "session1",
  time = lubridate::as_datetime(lubridate::today() - 3)
)

data_storage$read_event_data()
#> # A tibble: 4 × 8
#>   time                app_name session  type     id    value date       username
#>   <dttm>              <chr>    <chr>    <chr>    <chr> <chr> <date>     <chr>   
#> 1 2026-05-19 15:17:15 example  session1 test_ev… NA    NA    2026-05-19 NA      
#> 2 2026-05-19 15:17:15 example  s1       input    id1   NA    2026-05-19 NA      
#> 3 2026-05-19 15:17:15 example  s1       input    id2   32    2026-05-19 NA      
#> 4 2026-05-16 00:00:00 example  session1 test_ev… NA    NA    2026-05-16 NA      
data_storage$read_event_data(Sys.Date() - 1, Sys.Date() + 1)
#> # A tibble: 3 × 8
#>   time                app_name session  type     id    value date       username
#>   <dttm>              <chr>    <chr>    <chr>    <chr> <chr> <date>     <chr>   
#> 1 2026-05-19 15:17:15 example  session1 test_ev… NA    NA    2026-05-19 NA      
#> 2 2026-05-19 15:17:15 example  s1       input    id1   NA    2026-05-19 NA      
#> 3 2026-05-19 15:17:15 example  s1       input    id2   32    2026-05-19 NA      

file.remove(db_path)
#> [1] TRUE
```
