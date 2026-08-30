# Gather data columns into key-value pairs

Reformat `viewr` data into a "tidy" format so that every row corresponds
to the position (and potentially rotation) of a single subject during an
observed frame and time.

## Usage

``` r
gather_tunnel_data(obj_name, NA_drop = TRUE, ...)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- NA_drop:

  Should rows with NAs be dropped? Defaults to `TRUE`

- ...:

  Additional arguments that can be passed to other `pathviewr` functions
  such as
  [`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md)
  or
  [`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)

## Value

A tibble in "tidy" format which is formatted to have every row
correspond to the position (and potentially rotation) of a single
subject during an observed frame and time. Subjects' names are
automatically parsed from original variable names (e.g.
subject1_rotation_width extracts "subject1" as the subject name) and
stored in a `Subjects` column in the returned tibble.

## Details

The tibble or data.frame that is fed in must have variables that have
subject names and axis names separated by underscores. Axis names must
be one of the following: `position_length`, `position_width`, or
`position_height`. Each of these three dimensions must be present in the
data. Collectively, this means that names like `bird01_position_length`
or `larry_position_height` are acceptable, but `bird01_x` or
`bird01_length` are not.

## See also

Other data cleaning functions:
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
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

## First use relabel_viewr_axes() to rename these variables using _length,
## _width, and _height instead
motive_data_relabeled <- relabel_viewr_axes(motive_data)

## Now use gather_tunnel_data() to gather colums into tidy format
motive_data_gathered <- gather_tunnel_data(motive_data_relabeled)

## Column names reflect the way in which data were reformatted:
names(motive_data_gathered)
#>  [1] "frame"             "time_sec"          "subject"          
#>  [4] "position_length"   "position_width"    "position_height"  
#>  [7] "rotation_length"   "rotation_width"    "rotation_height"  
#> [10] "rotation_real"     "mean_marker_error"
```
