# Data storage class with MongoDB provider

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to MongoDB backend using a unified API for read/write
operations

## Super class

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\> `DataStorageMongoDB`

## Methods

### Public methods

- [`DataStorageMongoDB$new()`](#method-DataStorageMongoDB-new)

- [`DataStorageMongoDB$clone()`](#method-DataStorageMongoDB-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStorageMongoDB$new(
      hostname = "localhost",
      port = 27017,
      username = NULL,
      password = NULL,
      authdb = NULL,
      dbname = "shiny_telemetry",
      options = NULL,
      ssl_options = mongolite::ssl_options()
    )

#### Arguments

- `hostname`:

  the hostname or IP address of the MongoDB server.

- `port`:

  the port number of the MongoDB server (default is 27017).

- `username`:

  the username for authentication (optional).

- `password`:

  the password for authentication (optional).

- `authdb`:

  the default authentication database (optional).

- `dbname`:

  name of database (default is "shiny_telemetry").

- `options`:

  Additional connection options in a named list format (e.g., list(ssl =
  "true", replicaSet = "myreplicaset")) (optional).

- `ssl_options`:

  additional connection options such as SSL keys/certs (default is
  [`mongolite::ssl_options()`](https://jeroen.r-universe.dev/mongolite/reference/ssl_options.html)).

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorageMongoDB$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
data_storage <- DataStorageMongoDB$new(
  host = "localhost",
  db = "test",
  ssl_options = mongolite::ssl_options()
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
