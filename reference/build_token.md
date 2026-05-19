# Builds hash for a call

Function that takes creates a signature for the `values` using a secret.

## Usage

``` r
build_token(values, secret = NULL)
```

## Arguments

- values:

  R object that is going to be signed

- secret:

  string that contains the shared secret to sign the communication. It
  can be NULL on both telemetry and in plumber API to disable this
  communication feature

## Value

A string that contains an hash to uniquely identify the parameters.

## Details

This is used in shiny.telemetry, but also externally with the Plumber
endpoint.

## Examples

``` r
build_token(values = list(list(1, 2, 3), 2, 2, 3, "bb"))
#> [1] "99f110fffdfcbd97e98013a44f0eb0696f7b889699d8a1ee342ab6312e391652"
build_token(values = list(list(1, 2, 3), 1, 2, 3, "bb"))
#> [1] "2d28d1fa15dd69df1e922fbddf01c0991d6bdb10ac408a5fcb5f14f6b52229a1"
build_token(values = list(list(1, 2, 3), 1, 2, 3, "bb"), secret = "abc")
#> [1] "96425c9eceb7304f78a1b281252d3410634313e703d386b09776351ef974b292"
build_token(values = list(list(1, 2, 3), 1, 2, 3, "bb"), secret = "abd")
#> [1] "f26e6db10cc6dba5bfdc101bd3b9ce12d06bf109e148b2a4460807f1275dafcc"
```
