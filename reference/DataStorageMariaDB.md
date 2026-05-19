# Data storage class with MariaDB / MySQL provider

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to MariaDB backend using a unified API for read/write
operations

## Super classes

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\>
[`shiny.telemetry::DataStorageSQLFamily`](https://appsilon.github.io/shiny.telemetry/reference/DataStorageSQLFamily.md)
-\> `DataStorageMariaDB`

## Methods

### Public methods

- [`DataStorageMariaDB$new()`](#method-DataStorageMariaDB-new)

- [`DataStorageMariaDB$clone()`](#method-DataStorageMariaDB-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStorageMariaDB$new(
      username = NULL,
      password = NULL,
      hostname = "127.0.0.1",
      port = 3306,
      dbname = "shiny_telemetry"
    )

#### Arguments

- `username`:

  string with a MariaDB username.

- `password`:

  string with the password for the username.

- `hostname`:

  string with hostname of MariaDB instance.

- `port`:

  numeric value with the port number of MariaDB instance.

- `dbname`:

  string with the name of the database in the MariaDB instance.

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorageMariaDB$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
data_storage <- DataStorageMariaDB$new(user = "mariadb", password = "mysecretpassword")

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
