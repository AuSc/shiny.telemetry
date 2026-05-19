# Data storage class with MS SQL Server provider

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to MS SQL Server backend using a unified API for read/write
operations. This provider requires a configured and named `ODBC` driver
to be set up on your system, for example, "`ODBC` Driver 17 for SQL
Server" or "`ODBC` Driver 18 for SQL Server".

Note that MS SQL Server support requires a subtly different database
schema: the `time` field is stored as a `DATETIME` rather than a
`TIMESTAMP`.

## Super classes

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\>
[`shiny.telemetry::DataStorageSQLFamily`](https://appsilon.github.io/shiny.telemetry/reference/DataStorageSQLFamily.md)
-\> `DataStorageMSSQLServer`

## Methods

### Public methods

- [`DataStorageMSSQLServer$new()`](#method-DataStorageMSSQLServer-new)

- [`DataStorageMSSQLServer$clone()`](#method-DataStorageMSSQLServer-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStorageMSSQLServer$new(
      username = NULL,
      password = NULL,
      hostname = "127.0.0.1",
      port = 1433,
      dbname = "shiny_telemetry",
      driver = "ODBC Driver 17 for SQL Server",
      trust_server_certificate = "NO"
    )

#### Arguments

- `username`:

  string with a MS SQL Server username.

- `password`:

  string with the password for the username.

- `hostname`:

  string with hostname of the MS SQL Server instance.

- `port`:

  numeric value with the port number of MS SQL Server instance.

- `dbname`:

  string with the name of the database in the MS SQL Server instance.

- `driver`:

  string with the name of the `ODBC` driver class for MS SQL, for
  example "`ODBC` Driver 17 for SQL Server".

- `trust_server_certificate`:

  string with "NO" or "YES", setting whether or not to trust the
  server's certificate implicitly.

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorageMSSQLServer$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
data_storage <- DataStorageMSSQLServer$new(
  user = "sa",
  password = "my-Secr3t_Password",
  hostname = "localhost",
  port = 1433,
  dbname = "shiny_telemetry",
  driver = "ODBC Driver 18 for SQL Server",
  trust_server_certificate = "YES"
)

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
