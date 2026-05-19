# Data storage abstract class for SQL providers

Abstract subclass of the
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
R6 class for the SQL family of providers

## Super class

[`shiny.telemetry::DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
-\> `DataStorageSQLFamily`

## Methods

### Public methods

- [`DataStorageSQLFamily$clone()`](#method-DataStorageSQLFamily-clone)

Inherited methods

- [`shiny.telemetry::DataStorage$close()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-close)
- [`shiny.telemetry::DataStorage$initialize()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-initialize)
- [`shiny.telemetry::DataStorage$insert()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-insert)
- [`shiny.telemetry::DataStorage$read_event_data()`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.html#method-read_event_data)

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DataStorageSQLFamily$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
