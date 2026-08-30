# Relabel the dimensions as length, width, and height

Axes are commonly labeled as "x", "y", and "z" in recording software yet
`pathviewr` functions require these to be labeled as "length", "width",
and "height". `relabel_viewr_axes()` is a function that takes a `viewr`
object and allows the user to rename its variables.

## Usage

``` r
relabel_viewr_axes(
  obj_name,
  tunnel_length = "_z",
  tunnel_width = "_x",
  tunnel_height = "_y",
  real = "_w",
  ...
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- tunnel_length:

  The dimension that corresponds to tunnel length. Set to
  `tunnel_length = "_z"` by default. Argument should contain a character
  vector with a leading underscore (see Details)

- tunnel_width:

  The dimension that corresponds to tunnel width. Follows the same
  conventions as `tunnel_length` and defaults to `tunnel_length = "_x"`

- tunnel_height:

  The dimension that corresponds to tunnel height. Follows the same
  conventions as `tunnel_length` and defaults to `tunnel_length = "_y"`

- real:

  The dimension that corresponds to the "real" parameter in quaternion
  notation (for data with "rotation" values). Follows the same
  conventions as `tunnel_length` and defaults to `real = "_w"`

- ...:

  Additional arguments to be passed to
  [`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md).

## Value

A tibble or data.frame with variables that have been renamed.

## Details

Each argument must have a leading underscore ("\_") and each argument
must have an entry. E.g. tunnel_length = "\_Y" will replace all
instances of \_Y with \_length in the names of variables.

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

## Author

Vikram B. Baliga

## Examples

``` r

library(pathviewr)

## Import the Motive example data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

## Names of variables are labeled with _x, _y, _z, which we'd like to rename
names(motive_data)
#>  [1] "frame"                      "time_sec"                  
#>  [3] "device02_rotation_x"        "device02_rotation_y"       
#>  [5] "device02_rotation_z"        "device02_rotation_w"       
#>  [7] "device02_position_x"        "device02_position_y"       
#>  [9] "device02_position_z"        "device02_mean_marker_error"
#> [11] "device03_rotation_x"        "device03_rotation_y"       
#> [13] "device03_rotation_z"        "device03_rotation_w"       
#> [15] "device03_position_x"        "device03_position_y"       
#> [17] "device03_position_z"        "device03_mean_marker_error"
#> [19] "device05_rotation_x"        "device05_rotation_y"       
#> [21] "device05_rotation_z"        "device05_rotation_w"       
#> [23] "device05_position_x"        "device05_position_y"       
#> [25] "device05_position_z"        "device05_mean_marker_error"

## Now use relabel_viewr_axes() to rename these variables using _length,
## _width, and _height instead
motive_data_relabeled <-
  relabel_viewr_axes(motive_data,
                     tunnel_length = "_z",
                     tunnel_width = "_x",
                     tunnel_height = "_y",
                     real = "_w")

## See the result
names(motive_data_relabeled)
#>  [1] "frame"                      "time_sec"                  
#>  [3] "device02_rotation_width"    "device02_rotation_height"  
#>  [5] "device02_rotation_length"   "device02_rotation_real"    
#>  [7] "device02_position_width"    "device02_position_height"  
#>  [9] "device02_position_length"   "device02_mean_marker_error"
#> [11] "device03_rotation_width"    "device03_rotation_height"  
#> [13] "device03_rotation_length"   "device03_rotation_real"    
#> [15] "device03_position_width"    "device03_position_height"  
#> [17] "device03_position_length"   "device03_mean_marker_error"
#> [19] "device05_rotation_width"    "device05_rotation_height"  
#> [21] "device05_rotation_length"   "device05_rotation_real"    
#> [23] "device05_position_width"    "device05_position_height"  
#> [25] "device05_position_length"   "device05_mean_marker_error"
```
