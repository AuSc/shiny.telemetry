# Data Storage abstract class to handle all the read/write operations

Abstract R6 Class that encapsulates all the operations needed by
Shiny.telemetry to read and write. This removes the complexity from the
functions and uses a unified API.

## Active bindings

- `event_bucket`:

  string that identifies the bucket to store user related and action
  data

## Methods

### Public methods

- [`DataStorage$new()`](#method-DataStorage-new)

- [`DataStorage$insert()`](#method-DataStorage-insert)

- [`DataStorage$read_event_data()`](#method-DataStorage-read_event_data)

- [`DataStorage$close()`](#method-DataStorage-close)

- [`DataStorage$clone()`](#method-DataStorage-clone)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

initialize data storage object common with all providers

#### Usage

    DataStorage$new()

------------------------------------------------------------------------

### Method `insert()`

Insert new data

#### Usage

    DataStorage$insert(app_name, type, session = NULL, details = NULL, time = NULL)

#### Arguments

- `app_name`:

  string with name of dashboard (the version can be also included in
  this string)

- `type`:

  string that identifies the event type to store

- `session`:

  (optional) string that identifies a session where the event was logged

- `details`:

  atomic element of list with data to save in storage

- `time`:

  date time value indicates the moment the record was generated in UTC.
  By default it should be NULL and determined automatically, but in
  cases where it should be defined, use
  [`Sys.time()`](https://rdrr.io/r/base/Sys.time.html) or
  `lubridate::now(tzone = "UTC")` to generate it.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `read_event_data()`

read all user data from SQLite.

#### Usage

    DataStorage$read_event_data(date_from = NULL, date_to = NULL, app_name = NULL)

#### Arguments

- `date_from`:

  (optional) date representing the starting day of results.

- `date_to`:

  (optional) date representing the last day of results.

- `app_name`:

  (optional) string identifying the Dashboard-specific event data

------------------------------------------------------------------------

### Method [`close()`](https://rdrr.io/r/base/connections.html)

Close the connection if necessary

#### Usage

    DataStorage$close()

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorage$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
