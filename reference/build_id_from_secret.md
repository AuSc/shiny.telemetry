# Builds id from a secret that can be used in open communication

This is used in shiny.telemetry, but also externally with the Plumber
endpoint.

## Usage

``` r
build_id_from_secret(secret)
```

## Arguments

- secret:

  string that contains information that should not be publicly available

## Value

A string with an hash of the secret.

## Examples

``` r
build_id_from_secret("some_random_secret_generated_with_uuid::UUIDgenerate")
#> [1] "830cc11b"
```
