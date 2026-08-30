# "Center" the tunnel data, i.e. translation but no rotation

Redefine the center `(0, 0, 0,)` of the tunnel data via translating
positions along axes.

## Usage

``` r
redefine_tunnel_center(
  obj_name,
  axes = c("position_length", "position_width", "position_height"),
  length_method = c("original", "middle", "median", "user-defined"),
  width_method = c("original", "middle", "median", "user-defined"),
  height_method = c("original", "middle", "median", "user-defined"),
  length_zero = NA,
  width_zero = NA,
  height_zero = NA,
  ...
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- axes:

  Names of axes to be centered

- length_method:

  Method for length

- width_method:

  Method for width

- height_method:

  Method for height

- length_zero:

  User-defined value

- width_zero:

  User-defined value

- height_zero:

  User-defined value

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) in which data have been translated according to
the user's inputs, generally with `(0, 0, 0,)` being relocated to the
center of the tunnel.

## Details

For each `_method` argument, there are four choices of how centering is
handled: 1) "original" keeps axis as is – this is how width and
(possibly) height should be handled for flydra data; 2) "middle" is the
middle of the range of data: (min + max) / 2; 3) "median" is the median
value of data on that axis. Probably not recommended; and 4)
"user-defined" lets the user customize where the (0, 0, 0) point in the
tunnel will end up. Each `_zero` argument is subtracted from its
corresponding axis' data.

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
[`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

Other tunnel standardization functions:
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md)

## Author

Vikram B. Baliga

## Examples

``` r
## Import the Flydra example data included in
## the package
flydra_data <-
  read_flydra_mat(
    system.file("extdata",
                "pathviewr_flydra_example_data.mat",
                package = 'pathviewr'),
    subject_name = "birdie_wooster"
  )

## Re-center the Flydra data set.
## Width will be untouched
## Length will use the "middle" definition
## And height will be user-defined to be
## zeroed at 1.44 on the original axis
flydra_centered <-
  flydra_data %>%
  redefine_tunnel_center(length_method = "middle",
                         height_method = "user-defined",
                         height_zero = 1.44)
```
