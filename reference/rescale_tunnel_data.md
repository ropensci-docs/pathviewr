# Rescale position data within a `viewr` object

Should data have been exported at an incorrect scale, apply an isometric
transformation to the position data and associated mean marker errors
(if found)

## Usage

``` r
rescale_tunnel_data(obj_name, original_scale = 0.5, desired_scale = 1, ...)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"` that has been passed through
  [`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md)
  and
  [`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md)
  (or is structured as though it has been passed through those
  functions).

- original_scale:

  The original scale at which data were exported. See Details if
  unknown.

- desired_scale:

  The desired scale

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A `viewr` object that has position data (and `mean_marker_error data`,
if found) adjusted by the ratio of `desired_scale/original_scale`.

## Details

The `desired_scale` is divided by the `original_scale` to determine a
`scale_ratio` internally. If the `original_scale` is not explicitly
known, set it to 1 and then set `desired_scale` to be whatever scaling
ratio you have in mind. E.g. setting `original_scale` to 1 and then
`desired_scale` to 0.7 will multiply all position axis values by 0.7.

The default arguments of `original_scale = 0.5` and `desired_scale = 1`
apply a doubling of tunnel size isometrically.

## Author

Vikram B. Baliga

## Examples

``` r
## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

## Clean the file. It is generally recommended to clean up to the
## "gather" step before running rescale_tunnel_data().
 motive_gathered <-
   motive_data %>%
   relabel_viewr_axes() %>%
   gather_tunnel_data()

## Now rescale the tunnel data
motive_rescaled <-
  motive_gathered %>%
  rescale_tunnel_data(original_scale = 0.5,
                      desired_scale = 1)

## See the difference in data range e.g. for length
range(motive_rescaled$position_length)
#> [1] 0.07131 5.35294
range(motive_gathered$position_length)
#> [1] 0.035655 2.676470
```
