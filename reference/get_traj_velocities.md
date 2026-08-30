# Recompute trajectory-specific velocities

Recompute trajectory-specific velocities

## Usage

``` r
get_traj_velocities(
  obj_name,
  time_col = "time_sec",
  length_col = "position_length",
  width_col = "position_width",
  height_col = "position_height",
  set_init_vel_zero = FALSE,
  velocity_min = NA,
  velocity_max = NA
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- time_col:

  Name of the column containing time

- length_col:

  Name of the column containing length dimension

- width_col:

  Name of the column containing width dimension

- height_col:

  Name of the column containing height dimension

- set_init_vel_zero:

  Should the first value be zero or can it be a duplicate of the second
  velocity value? Defaults to FALSE.

- velocity_min:

  Should data below a certain velocity be filtered out of the object? If
  so, enter a numeric. If not, keep NA.

- velocity_max:

  Should data above a certain velocity be filtered out of the object? If
  so, enter a numeric. If not, keep NA.

## Value

If `add_to_viewr` is `TRUE`, additional columns are appended to the
input viewr object. If `FALSE`, a standalone tibble is created. Either
way, an "instantaneous" velocity is computed as the difference in
position divided by the difference in time as each successive row is
encountered. Additionally, velocities along each of the three position
axes are computed and provided as additional columns.

## Details

Instantaneous velocity is not truly "instantaneous" but rather is
approximated as the change in distance divided by change in time from
one observation (row) to the previous observation (row). Each component
of velocity is computed (i.e. per axis) along with the overall velocity
of the subject.

## See also

Other mathematical functions:
[`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md),
[`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
[`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md),
[`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md),
[`get_3d_cross_prod()`](https://docs.ropensci.org/pathviewr/reference/get_3d_cross_prod.md),
[`get_dist_point_line()`](https://docs.ropensci.org/pathviewr/reference/get_dist_point_line.md),
[`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md),
[`rad_2_deg()`](https://docs.ropensci.org/pathviewr/reference/rad_2_deg.md)

## Author

Vikram B. Baliga
