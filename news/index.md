# Changelog

## shiny.telemetry 0.3.1.9002

#### New Features

- Added a dropdown to the
  [`analytics_app()`](https://appsilon.github.io/shiny.telemetry/reference/analytics_app.md)
  to switch between applications.
- Resolve bug#192 that ignored excluded input regex.

#### Bug Fixes

- Fixed problem with concurrent writes in log file backend.

## shiny.telemetry 0.3.1

CRAN release: 2024-10-15

#### New Features

- Added `log_errors` method that allows users to track errors in their
  Shiny apps outside `start_session`
  ([\#189](https://github.com/Appsilon/shiny.telemetry/issues/189)).

#### Bug Fixes

- Fixed problem with `log_all_inputs` call that crashed telemetry
  ([\#187](https://github.com/Appsilon/shiny.telemetry/issues/187)).
- Fixed error appearing in analytics app
  ([\#188](https://github.com/Appsilon/shiny.telemetry/issues/188)).

## shiny.telemetry 0.3.0

CRAN release: 2024-07-17

#### New Features

- Added shiny error tracking (activated by default with `start_session`)
  ([\#116](https://github.com/Appsilon/shiny.telemetry/issues/116)).
- Updated `get_user` method to retrieve user in `shinyproxy` environment
  ([\#124](https://github.com/Appsilon/shiny.telemetry/issues/124)).
- Added flexibility to select between \[`RPostgreSQL`, `RPostgres`\]
  drivers
  ([\#147](https://github.com/Appsilon/shiny.telemetry/issues/147)).
- Improved input tracking by implementing inclusion and exclusion logic
  ([\#30](https://github.com/Appsilon/shiny.telemetry/issues/30)).
- Added tracking for returning anonymous users
  ([\#142](https://github.com/Appsilon/shiny.telemetry/issues/142)).
- Added support for MongoDB (see `DataStorageMongoDB` class)
  ([\#174](https://github.com/Appsilon/shiny.telemetry/issues/174)).

#### Miscellaneous

- Updates documentation to use markdown format
  ([\#153](https://github.com/Appsilon/shiny.telemetry/issues/153)).
- Improves SQL injection safeguards via
  [`glue::glue_sql`](https://glue.tidyverse.org/reference/glue_sql.html)
  to generated SQL queries
  ([\#34](https://github.com/Appsilon/shiny.telemetry/issues/34)).
- Show proper error message when no telemetry data is available
  ([\#177](https://github.com/Appsilon/shiny.telemetry/issues/177)).
- Adds how-to guides to site
  ([\#179](https://github.com/Appsilon/shiny.telemetry/issues/179) and
  [\#180](https://github.com/Appsilon/shiny.telemetry/issues/180))

#### Bug Fixes

- Fixed Analytics app not being able to access data by Instrumentation
  app ([\#164](https://github.com/Appsilon/shiny.telemetry/issues/164)).
- Fixed SQLite data storage backend when reading date column
  ([\#182](https://github.com/Appsilon/shiny.telemetry/issues/182)).

## shiny.telemetry 0.2.0

CRAN release: 2023-11-16

#### New Features

- Allowed optional username overwrite
  ([\#123](https://github.com/Appsilon/shiny.telemetry/issues/123)).
- Added MS SQL Server support (see `DataStorageMSSQLServer` class)
  ([\#128](https://github.com/Appsilon/shiny.telemetry/issues/128)).
- Added CI tests to all `DBI`-based `DataStorage` providers
  ([\#129](https://github.com/Appsilon/shiny.telemetry/issues/129)).
- Added optional parameter to `read_event_data` that filters by
  `app_name`
  ([\#129](https://github.com/Appsilon/shiny.telemetry/issues/129)).

#### Bug fixes

- Fixed the way of getting the session token
  ([\#120](https://github.com/Appsilon/shiny.telemetry/issues/120)).
- Fixed loading of complex nested payloads
  ([\#133](https://github.com/Appsilon/shiny.telemetry/issues/133)).

#### Miscellaneous

- Added `pre-commit` hooks
  ([\#140](https://github.com/Appsilon/shiny.telemetry/issues/140)).

## shiny.telemetry 0.1.0

CRAN release: 2023-05-05

- First release
