# Extract header info from imported viewr object

A function to quickly return the information stored in the header of the
original data file imported via `pathviewr`'s `read_` functions.

## Usage

``` r
get_header_viewr(obj_name, ...)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"` `pathviewr_steps`

- ...:

  Additional arguments that may be passed to other `pathviewr` functions

## Value

The value of the `header` attribute, or NULL if no exact match is found
and no or more than one partial match is found.

## Author

Vikram B. Baliga

## Examples

``` r
library(pathviewr)

## Import the Motive example data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

## Now display the Header information
get_header_viewr(motive_data)
#>                 metadata                      value
#> 1         Format Version                       1.23
#> 2              Take Name  sept-18_mixed-group_16-30
#> 3             Take Notes                           
#> 4     Capture Frame Rate                 100.000000
#> 5      Export Frame Rate                 100.000000
#> 6     Capture Start Time 2019-09-18 04.30.02.695 PM
#> 7   Total Frames in Take                     190951
#> 8  Total Exported Frames                     190951
#> 9          Rotation Type                 Quaternion
#> 10          Length Units                     Meters
#> 11      Coordinate Space                     Global
```
