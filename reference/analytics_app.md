# Run example telemetry analytics dashboard

Run example telemetry analytics dashboard

## Usage

``` r
analytics_app(data_storage)
```

## Arguments

- data_storage:

  data_storage instance that will handle all backend read and writes.

## Value

An object that represents the analytics app. Printing the object or
passing it to
[`shiny::runApp()`](https://rdrr.io/pkg/shiny/man/runApp.html) will run
it.
