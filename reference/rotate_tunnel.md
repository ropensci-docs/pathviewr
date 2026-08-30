# Rotate a tunnel so that perches are approximately aligned

The rotation is applied about the height axis and affects tunnel length
and width only, i.e. no rotation of height.

## Usage

``` r
rotate_tunnel(
  obj_name,
  all_heights_min = 0.11,
  all_heights_max = 0.3,
  perch1_len_min = -0.06,
  perch1_len_max = 0.06,
  perch2_len_min = 2.48,
  perch2_len_max = 2.6,
  perch1_wid_min = 0.09,
  perch1_wid_max = 0.31,
  perch2_wid_min = 0.13,
  perch2_wid_max = 0.35,
  ...
)
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

- all_heights_min:

  Minimum perch height

- all_heights_max:

  Maximum perch height

- perch1_len_min:

  Minimum length value of perch 1

- perch1_len_max:

  Maximum length value of perch 1

- perch2_len_min:

  Minimum length value of perch 2

- perch2_len_max:

  Maximum length value of perch 2

- perch1_wid_min:

  Minimum width value of perch 1

- perch1_wid_max:

  Maximum width value of perch 1

- perch2_wid_min:

  Minimum width value of perch 2

- perch2_wid_max:

  Maximum width value of perch 2

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) in which data have been rotated according to
user specifications.

## Details

The user first estimates the locations of the perches by specifying
bounds for where each perch is located. The function then computes the
center of each bounding box and estimates that to be the midpoint of
each perch. Then the center point of the tunnel (center between the
perch midpoints) is estimated. The angle between perch1_center,
tunnel_center_point, and arbitrary point along the length axis
(tunnel_center_point - 1 on length) is estimated. That angle is then
used to rotate the data, again only in the length and width dimensions.
Height is standardized by (approximate) perch height; values greater
than 0 are above the perch and values less than 0 are below the perch
level.

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
[`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

Other tunnel standardization functions:
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md)

## Author

Vikram B. Baliga

## Examples

``` r
## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                              package = 'pathviewr'))

## Clean the file. It is generally recommended to clean up to the
## "trimmed" step before running rotate_tunnel().
motive_trimmed <-
  motive_data %>%
  relabel_viewr_axes() %>%
  gather_tunnel_data() %>%
  trim_tunnel_outliers()

## Now rotate the tunnel using default values
motive_rotated <-
  motive_trimmed %>%
  rotate_tunnel()

## The following attributes store information about
## how rotation & translation was applied
attr(motive_rotated, "rotation_degrees")
#> [1] 0.9022212
attr(motive_rotated, "rotation_radians")
#> [1] 0.01574673
attr(motive_rotated, "perch1_midpoint_original")
#> [1] 0.000 0.200 0.205
attr(motive_rotated, "perch1_midpoint_current")
#> [1] -1.270157e+00  4.645589e-15  2.050000e-01
attr(motive_rotated, "tunnel_centerpoint_original")
#> [1] 1.270 0.220 0.205
attr(motive_rotated, "perch2_midpoint_original")
#> [1] 2.540 0.240 0.205
attr(motive_rotated, "perch2_midpoint_current")
#> [1]  1.270157e+00 -4.645589e-15  2.050000e-01
```
