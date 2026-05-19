# Telemetry class to manage analytics gathering at a global level

An instance of this class will define metadata and data storage provider
for gathering telemetry analytics of a Shiny dashboard.

The `name` and `version` parameters will describe the dashboard name and
version to track using analytics, allowing to store the analytics data
from multiple dashboards in the same data storage provider. As well as
discriminate different versions of the dashboard.

The default data storage provider uses a local SQLite database, but this
can be customizable when instantiating the class, by using another one
of the supported providers (see
[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)).

## Debugging

Events are logged at the `DEBUG` level using the `logger` package. To
see the logs, you can set:

    logger::log_threshold("DEBUG", namespace = "shiny.telemetry")

## See also

[`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md)
which this function wraps.

## Active bindings

- `data_storage`:

  instance of a class that inherits from
  [`DataStorage`](https://appsilon.github.io/shiny.telemetry/reference/DataStorage.md).
  See the documentation on that class for more information.

- `app_name`:

  string with name of dashboard

## Methods

### Public methods

- [`Telemetry$new()`](#method-Telemetry-new)

- [`Telemetry$start_session()`](#method-Telemetry-start_session)

- [`Telemetry$log_navigation()`](#method-Telemetry-log_navigation)

- [`Telemetry$log_navigation_manual()`](#method-Telemetry-log_navigation_manual)

- [`Telemetry$log_login()`](#method-Telemetry-log_login)

- [`Telemetry$log_logout()`](#method-Telemetry-log_logout)

- [`Telemetry$log_click()`](#method-Telemetry-log_click)

- [`Telemetry$log_browser_version()`](#method-Telemetry-log_browser_version)

- [`Telemetry$log_button()`](#method-Telemetry-log_button)

- [`Telemetry$log_all_inputs()`](#method-Telemetry-log_all_inputs)

- [`Telemetry$log_input()`](#method-Telemetry-log_input)

- [`Telemetry$log_input_manual()`](#method-Telemetry-log_input_manual)

- [`Telemetry$log_custom_event()`](#method-Telemetry-log_custom_event)

- [`Telemetry$log_error()`](#method-Telemetry-log_error)

- [`Telemetry$log_errors()`](#method-Telemetry-log_errors)

- [`Telemetry$clone()`](#method-Telemetry-clone)

------------------------------------------------------------------------

### Method [`new()`](https://rdrr.io/r/methods/new.html)

Constructor that initializes Telemetry instance with parameters.

#### Usage

    Telemetry$new(
      app_name = "(dashboard)",
      data_storage = DataStorageSQLite$new(db_path = file.path("telemetry.sqlite"))
    )

#### Arguments

- `app_name`:

  (optional) string that identifies the name of the dashboard. By
  default it will store data with `(dashboard)`.

- `data_storage`:

  (optional) `DataStorage` instance where telemetry data is being
  stored. It can take any of data storage providers by this package, By
  default it will store in a SQLite local database in the current
  working directory with filename `telemetry.sqlite`

- `version`:

  (optional) string that identifies the version of the dashboard. By
  default it will use `v0.0.0`.

------------------------------------------------------------------------

### Method `start_session()`

Setup basic telemetry

#### Usage

    Telemetry$start_session(
      track_inputs = TRUE,
      track_values = FALSE,
      login = TRUE,
      logout = TRUE,
      browser_version = TRUE,
      navigation_input_id = NULL,
      session = shiny::getDefaultReactiveDomain(),
      username = NULL,
      track_anonymous_user = TRUE,
      track_errors = TRUE
    )

#### Arguments

- `track_inputs`:

  flag that indicates if the basic telemetry should track the inputs
  that change value. `TRUE` by default

- `track_values`:

  flag that indicates if the basic telemetry should track the values of
  the inputs that are changing. `FALSE` by default. This parameter is
  ignored if `track_inputs` is `FALSE`

- `login`:

  flag that indicates if the basic telemetry should track when a session
  starts. `TRUE` by default.

- `logout`:

  flag that indicates if the basic telemetry should track when the
  session ends. `TRUE` by default.

- `browser_version`:

  flag that indicates that the browser version should be tracked.`TRUE`
  by default.

- `navigation_input_id`:

  string or vector of strings that represent input ids and which value
  should be tracked as navigation events. i.e. a change in the value
  represent a navigation to a page or tab. By default, no navigation is
  tracked.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

- `username`:

  Character with username. If set, it will overwrite username from
  session object.

- `track_anonymous_user`:

  flag that indicates to track anonymous user. A cookie is used to track
  same user without login over multiple sessions, This is only activated
  if none of the automatic methods produce a username and when a
  username is not explicitly defined.`TRUE` by default.

- `track_errors`:

  flag that indicates if the basic telemetry should track the errors.
  `TRUE` by default. if using shiny version \< `1.8.1`, it can auto log
  errors only in UI output functions. By using latest versions of shiny,
  it can auto log all types of errors.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_navigation()`

Log an input change as a navigation event

#### Usage

    Telemetry$log_navigation(input_id, session = shiny::getDefaultReactiveDomain())

#### Arguments

- `input_id`:

  string that identifies the generic input in the Shiny application so
  that the function can track and log changes to it.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_navigation_manual()`

Log a navigation event manually by indicating the id (as input id)

#### Usage

    Telemetry$log_navigation_manual(
      navigation_id,
      value,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `navigation_id`:

  string that identifies navigation event.

- `value`:

  string that indicates a value for the navigation

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_login()`

Log when session starts

#### Usage

    Telemetry$log_login(
      username = NULL,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `username`:

  string with username from current session

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_logout()`

Log when session ends

#### Usage

    Telemetry$log_logout(
      username = NULL,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `username`:

  string with username from current session

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_click()`

Log an action click

#### Usage

    Telemetry$log_click(id, session = shiny::getDefaultReactiveDomain())

#### Arguments

- `id`:

  string that identifies a manual click to the dashboard.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_browser_version()`

Log the browser version

#### Usage

    Telemetry$log_browser_version(session = shiny::getDefaultReactiveDomain())

#### Arguments

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_button()`

Track a button and track changes to this input (without storing the
values)

#### Usage

    Telemetry$log_button(
      input_id,
      track_value = FALSE,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `input_id`:

  string that identifies the button in the Shiny application so that the
  function can track and log changes to it.

- `track_value`:

  flag that indicates if the basic telemetry should track the value of
  the input that are changing. `FALSE` by default.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_all_inputs()`

Automatic tracking of all input changes in the App. Depending on the
parameters, it may only track a subset of inputs by excluding patterns
or by including specific vector of `input_ids`.

#### Usage

    Telemetry$log_all_inputs(
      track_values = FALSE,
      excluded_inputs = c("browser_version"),
      excluded_inputs_regex = NULL,
      include_input_ids = NULL,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `track_values`:

  flag that indicates if the basic telemetry should track the values of
  the inputs that are changing. `FALSE` by default. This parameter is
  ignored if `track_inputs` is `FALSE`.

- `excluded_inputs`:

  vector of input_ids that should not be tracked. By default it doesn't
  track browser version, which is added by this package.

- `excluded_inputs_regex`:

  vector of input_ids that should not be tracked. All Special characters
  will be escaped.

- `include_input_ids`:

  vector of input_ids that will be tracked. This input_ids should be an
  exact match and will be given priority over exclude list.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_input()`

Track changes of a specific input id.

#### Usage

    Telemetry$log_input(
      input_id,
      track_value = FALSE,
      matching_values = NULL,
      input_type = "text",
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `input_id`:

  string (or vector of strings) that identifies the generic input in the
  Shiny application so that the function can track and log changes to
  it.

  When the `input_id` is a vector of strings, the function will behave
  just as calling `log_input` one by one with the same arguments.

- `track_value`:

  flag that indicates if the basic telemetry should track the value of
  the input that are changing. `FALSE` by default.

- `matching_values`:

  An object specified possible values to register.

- `input_type`:

  `"text"` to registered bare input value, `"json"` to parse value from
  `JSON` format.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for its side effects.

------------------------------------------------------------------------

### Method `log_input_manual()`

Log a manual input value.

This can be called in telemetry and is also used as a layer between
log_input family of functions and actual log event. It creates the
correct payload to log the event internally.

#### Usage

    Telemetry$log_input_manual(
      input_id,
      value = NULL,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `input_id`:

  string that identifies the generic input in the Shiny application so
  that the function can track and log changes to it.

- `value`:

  (optional) scalar value or list with the value to register.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_custom_event()`

Log a manual event

#### Usage

    Telemetry$log_custom_event(
      event_type,
      details = NULL,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `event_type`:

  string that identifies the event type

- `details`:

  (optional) scalar value or list with the value to register.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_error()`

Log a manual error event

#### Usage

    Telemetry$log_error(
      output_id,
      message,
      session = shiny::getDefaultReactiveDomain()
    )

#### Arguments

- `output_id`:

  string that refers to the output element where the error occurred.

- `message`:

  string that describes the error.

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `log_errors()`

Track errors as they occur in observe and reactive

#### Usage

    Telemetry$log_errors(session = shiny::getDefaultReactiveDomain())

#### Arguments

- `session`:

  `ShinySession` object or NULL to identify the current Shiny session.

#### Returns

Nothing. This method is called for side effects.

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    Telemetry$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
log_file_path <- tempfile(fileext = ".txt")
telemetry <- Telemetry$new(
  data_storage = DataStorageLogFile$new(log_file_path = log_file_path)
) # 1. Initialize telemetry with default options

#
# Use in a shiny application

if (interactive()) {
  library(shiny)

  shinyApp(
    ui = fluidPage(
      use_telemetry(), # 2. Add necessary javascript to Shiny
      numericInput("n", "n", 1),
      plotOutput('plot')
    ),
    server = function(input, output) {
      telemetry$start_session() # 3. Minimal setup to track events
      output$plot <- renderPlot({ hist(runif(input$n)) })
    }
  )
}

#
# Manual logging of Telemetry that can be used inside Shiny Application
# to further customize the events to be tracked.

session <- shiny::MockShinySession$new() # Create dummy session (only for example purposes)
class(session) <- c(class(session), "ShinySession")

telemetry$log_click("a_button", session = session)

telemetry$log_error("global", message = "An error has occured")

telemetry$log_custom_event("a_button", list(value = 2023), session = session)
telemetry$log_custom_event("a_button", list(custom_field = 23), session = session)

# Manual call login with custom username
telemetry$log_login("ben", session = session)

# Read all data
telemetry$data_storage$read_event_data()
#> # A tibble: 5 × 11
#>   app_name    type   session id    output_id message value custom_field username
#>   <chr>       <chr>  <chr>   <chr> <chr>     <chr>   <chr> <chr>        <chr>   
#> 1 (dashboard) click  a82bb6… a_bu… NA        NA      NA    NA           NA      
#> 2 (dashboard) error  NA      NA    global    An err… NA    NA           NA      
#> 3 (dashboard) a_but… a82bb6… NA    NA        NA      2023  NA           NA      
#> 4 (dashboard) a_but… a82bb6… NA    NA        NA      NA    23           NA      
#> 5 (dashboard) login  a82bb6… NA    NA        NA      NA    NA           ben     
#> # ℹ 2 more variables: time <dttm>, date <date>

file.remove(log_file_path)
#> [1] TRUE

#
# Using SQLite

db_path <- tempfile(fileext = ".sqlite")
telemetry_sqlite <- Telemetry$new(
  data_storage = DataStorageSQLite$new(db_path = db_path)
)

telemetry_sqlite$log_custom_event("a_button", list(value = 2023), session = session)
telemetry_sqlite$log_custom_event("a_button", list(custom_field = 23), session = session)

# Read all data from time range
telemetry_sqlite$data_storage$read_event_data("2020-01-01", "2055-01-01")
#> # A tibble: 2 × 9
#>   time                app_name session type  value custom_field date       id   
#>   <dttm>              <chr>    <chr>   <chr> <chr> <chr>        <date>     <chr>
#> 1 2026-05-19 15:17:16 (dashbo… a82bb6… a_bu… 2023  NA           2026-05-19 NA   
#> 2 2026-05-19 15:17:16 (dashbo… a82bb6… a_bu… NA    23           2026-05-19 NA   
#> # ℹ 1 more variable: username <chr>

file.remove(db_path)
#> [1] TRUE
```
