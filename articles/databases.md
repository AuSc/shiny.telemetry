# Use External Databases with shiny.telemetry

The [shiny.telemetry](https://appsilon.github.io/shiny.telemetry/)
package can be used with any Shiny application and in this guide we will
show how to use it with different databases backend.

The following databases are supported by
[shiny.telemetry](https://appsilon.github.io/shiny.telemetry/):

- [PostgreSQL](https://www.postgresql.org/docs/current/index.html)
- [MariaDB](https://mariadb.org/documentation/) or
  [MySQL](https://dev.mysql.com/doc/refman/en/)
- [MS SQL Server](https://learn.microsoft.com/en-us/sql/sql-server/)
- [MongoDB](https://www.mongodb.com/docs/manual/)
- [SQLite](https://sqlite.org/docs.html)

A requirements to use
[shiny.telemetry](https://appsilon.github.io/shiny.telemetry/) with
external databases in a production environment is to have the database
server running and a user with the necessary permissions to insert. A
minimal setup should have a user that only has write/insert permissions
to the [shiny.telemetry](https://appsilon.github.io/shiny.telemetry/)
table storing the events. The read permission is only necessary for
processing the data, such as the default analytics dashboard that we
provide with the package (see
[`analytics_app()`](https://appsilon.github.io/shiny.telemetry/reference/analytics_app.md)).
This database setup can be done by an infrastructure team or the
database administrator.

We provide example applications for each database backend with necessary
R code to run both the application and the analytics server. This is
further supported with a `docker-container.yml` to help users quickly
setup and test the apps locally. It requires
[Docker](https://docs.docker.com/reference/) (`docker compose up -d`) or
[Podman](https://podman.io/docs) (`podman-compose up -d`) installed to
run the containers.

These applications are available under the `inst/examples/` folder or
via the [GitHub
link](https://github.com/Appsilon/shiny.telemetry/tree/main/inst/examples).

## Create a data storage backend

Each data storage backend will create the necessary tables *(or
“Collection” in the case of MongoDB)* with the respective schema when
needed.

The arguments to create an data storage instance vary, as different
databases require their own options. However, once the data storage
object is created, the read and write operations have the same API.

Below you find chunks to create a data storage object for each supported
database.

- PostgreSQL
- MariaDB / MySQL
- MS SQL Server
- MongoDB
- SQLite

``` r

Sys.setenv("POSTGRES_USER" = "postgres", "POSTGRES_PASS" = "mysecretpassword")
data_storage <- DataStoragePostgreSQL$new(
  user = Sys.getenv("POSTGRES_USER"),
  password = Sys.getenv("POSTGRES_PASS"),
  hostname = "127.0.0.1",
  port = 5432,
  dbname = "shiny_telemetry",
  driver = "RPostgreSQL"
)
```

*notes*:

- The `dbname` database needs to be created before running the
  application with
  [shiny.telemetry](https://appsilon.github.io/shiny.telemetry/);
- The `driver` allows users to use either
  [RPostgreSQL](https://github.com/tomoakin/RPostgreSQL) or
  [RPostgres](https://rpostgres.r-dbi.org) R packages;
- Never store passwords and other sensitive directly in code. Please use
  environment variables or other secure methods;
  - The `.Renviron` file is the default way in R of setting up
    environment variables *(instead of
    [`Sys.setenv()`](https://rdrr.io/r/base/Sys.setenv.html) as shown
    above for convenience)*.

To run PostgreSQL in a container locally, you can use the following
Docker compose file:
[`inst/examples/postgresql/docker-compose.yml`](https://github.com/Appsilon/shiny.telemetry/blob/main/inst/examples/postgresql/docker-compose.yml).

``` r

Sys.setenv("MARIADB_USER" = "mariadb", "MARIADB_PASS" = "mysecretpassword")
data_storage <- DataStorageMariaDB$new(
  user = Sys.getenv("MARIADB_USER"), 
  password = Sys.getenv("MARIADB_PASS"),
  hostname = "127.0.0.1",
  port = 3306,
  dbname = "shiny_telemetry"
)
```

*notes*:

- The `dbname` database needs to be created before running the
  application with
  [shiny.telemetry](https://appsilon.github.io/shiny.telemetry/);
- Never store usernames, passwords and other sensitive directly in code.
  Please use environment variables or other secure methods;
  - The `.Renviron` file is the default way in R of setting up
    environment variables *(instead of
    [`Sys.setenv()`](https://rdrr.io/r/base/Sys.setenv.html) as shown
    above for convenience)*.

To run MariaDB in a container locally, you can use the following Docker
compose file:
[`inst/examples/mariadb/docker-compose.yml`](https://github.com/Appsilon/shiny.telemetry/blob/main/inst/examples/mariadb/docker-compose.yml).

``` r

Sys.setenv(MSSQL_USER = "sa", MSSQL_PASS = "my-Secr3t_Password")
data_storage <- DataStorageMSSQLServer$new(
  user = Sys.getenv("MSSQL_USER"),
  password = Sys.getenv("MSSQL_PASS"),
  hostname = "127.0.0.1", 
  port = 1433,
  dbname = "my_db", 
  driver = "ODBC Driver 18 for SQL Server", 
  trust_server_certificate = "YES"
)
```

*notes*:

- The `dbname` database needs to be created before running the
  application with
  [shiny.telemetry](https://appsilon.github.io/shiny.telemetry/);
- Never store passwords and other sensitive directly in code. Please use
  environment variables or other secure methods;
  - The `.Renviron` file is the default way in R of setting up
    environment variables *(instead of
    [`Sys.setenv()`](https://rdrr.io/r/base/Sys.setenv.html) as shown
    above for convenience)*.

To run Microsoft SQL Server in a container locally, you can use the
following Docker compose file:
[`inst/examples/mssql/docker-compose.yml`](https://github.com/Appsilon/shiny.telemetry/blob/main/inst/examples/mssql/docker-compose.yml).

``` r
data_storage <- DataStorageMongoDB$new(
  host = "localhost",
  dbname = "test",
  authdb = NULL,
  options = NULL,
  ssl_options = mongolite::ssl_options()
)

To run MongoDB in a container locally, you can use the following Docker compose file: [`inst/examples/mssql/docker-compose.yml`](https://github.com/Appsilon/shiny.telemetry/blob/main/inst/examples/mongodb/docker-compose.yml).
```

``` r

data_storage <- DataStorageSQLite$new(
  db_path = "telemetry.sqlite"
)
```

Unlike the other database backends, SQLite only requires a path to a
file that the Shiny application can write to.

## Data storage usage in `{shiny.telemetry}`

The data storage API to read and write events for
[shiny.telemetry](https://appsilon.github.io/shiny.telemetry/) is
consistent across all backends, which allows the developer to implement
and test the package with the most convenient backend and then easily
migrate to an external database.

Therefore, once it is initialized it can be used to create the
`Telemetry` object and start a session.

``` r

# data_storage variable is initialized with one of the previous code chunks.
telemetry <- Telemetry$new(data_storage = data_storage) # 1. Initialize telemetry with object created above

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
```
