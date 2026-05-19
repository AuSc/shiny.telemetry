# Data storage class with SQLite provider

Implementation of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class to SQLite backend using a unified API for read/write operations

## Super class

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\> `DataStoragePlumber`

## Active bindings

- `event_read_endpoint`:

  string field that returns read action endpoint

- `event_insert_endpoint`:

  string field that returns insert action endpoint

## Methods

### Public methods

- [`DataStoragePlumber$new()`](#method-DataStoragePlumber-new)

- [`DataStoragePlumber$clone()`](#method-DataStoragePlumber-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Initialize the data storage class

#### Usage

    DataStoragePlumber$new(
      hostname = "127.0.0.1",
      port = 80,
      protocol = "http",
      path = NULL,
      secret = NULL,
      authorization = NULL
    )

#### Arguments

- `hostname`:

  string with hostname of plumber instance,

- `port`:

  numeric value with port number of plumber instance.

- `protocol`:

  string with protocol of the connection of the plumber instance.

- `path`:

  string with sub-path of plumber deployment.

- `secret`:

  string with secret to sign communication with plumber (can be NULL for
  disabling communication signing).

- `authorization`:

  string to use in HTTP headers for authorization (for example: to
  authenticate to a plumber deployment behind a connect server).

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStoragePlumber$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
# Make sure the PLUMBER_SECRET environment variable is valid before
# running these examples (NULL or a valid secret)

data_storage <- DataStoragePlumber$new(
  hostname = "connect.appsilon.com",
  path = "shiny_telemetry_plumber",
  port = 443,
  protocol = "https",
  authorization = Sys.getenv("CONNECT_AUTHORIZATION_KEY"),
  secret = Sys.getenv("PLUMBER_SECRET")
)

data_storage <- DataStoragePlumber$new(
  hostname = "127.0.0.1",
  path = NULL,
  port = 8087,
  protocol = "http",
  secret = Sys.getenv("PLUMBER_SECRET")
)

data_storage$insert("example", "test_event", "session1")
data_storage$insert("example", "input", "s1", list(id = "id"))
data_storage$insert("example", "input", "s1", list(id = "id2", value = 32))

data_storage$insert(
  "example", "test_event_3_days_ago", "session1",
  time = lubridate::as_datetime(lubridate::today() - 3)
)

data_storage$read_event_data()
data_storage$read_event_data(Sys.Date() - 1, Sys.Date() + 1)
} # }
```
