# Merge a list of regular expressions into a single one

Merge a list of regular expressions into a single one

## Usage

``` r
merge_excluded_regex(regex_l, trim_whitespace = TRUE)
```

## Arguments

- regex_l:

  list of regular expressions to be merged.

- trim_whitespace:

  boolean indicating if whitespace should be trim from the start and end
  of the regex list.

## Value

Single regular expression string.
