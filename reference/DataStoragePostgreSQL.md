# Data storage class with PostgreSQL provider

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to PostgreSQL backend using a unified API for read/write
operations

## Super classes

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\>
[`shiny.telemetry::DataStorageSQLFamily`](https://appsilon.github.io/shiny.telemetry/reference/DataStorageSQLFamily.md)
-\> `DataStoragePostgreSQL`

## Methods

### Public methods

- [`DataStoragePostgreSQL$new()`](#method-DataStoragePostgreSQL-new)

- [`DataStoragePostgreSQL$clone()`](#method-DataStoragePostgreSQL-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStoragePostgreSQL$new(
      username = NULL,
      password = NULL,
      hostname = "127.0.0.1",
      port = 5432,
      dbname = "shiny_telemetry",
      driver = "RPostgreSQL"
    )

#### Arguments

- `username`:

  string with a PostgreSQL username.

- `password`:

  string with the password for the username.

- `hostname`:

  string with hostname of PostgreSQL instance.

- `port`:

  numeric value with the port number of PostgreSQL instance.

- `dbname`:

  string with the name of the database in the PostgreSQL instance.

- `driver`:

  string, to select PostgreSQL driver among
  `c("RPostgreSQL", "RPostgres")`.

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStoragePostgreSQL$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
data_storage <- DataStoragePostgreSQL$new(user = "postgres", password = "mysecretpassword")

data_storage$insert("example", "test_event", "session1")
data_storage$insert("example", "input", "s1", list(id = "id1"))
data_storage$insert("example", "input", "s1", list(id = "id2", value = 32))

data_storage$insert(
  "example", "test_event_3_days_ago", "session1",
  time = lubridate::as_datetime(lubridate::today() - 3)
)

data_storage$read_event_data()
data_storage$read_event_data(Sys.Date() - 1, Sys.Date() + 1)
data_storage$close()
} # }
```
