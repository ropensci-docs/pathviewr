# Convert degrees to radians

Convert degrees to radians

## Usage

``` r
deg_2_rad(deg)
```

## Arguments

- deg:

  Degrees (a numeric of any length \>= 1)

## Value

The angle(s) in radians (as a numeric vector of the same length)

## See also

Other mathematical functions:
[`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
[`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md),
[`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md),
[`get_3d_cross_prod()`](https://docs.ropensci.org/pathviewr/reference/get_3d_cross_prod.md),
[`get_dist_point_line()`](https://docs.ropensci.org/pathviewr/reference/get_dist_point_line.md),
[`get_traj_velocities()`](https://docs.ropensci.org/pathviewr/reference/get_traj_velocities.md),
[`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md),
[`rad_2_deg()`](https://docs.ropensci.org/pathviewr/reference/rad_2_deg.md)

## Author

Vikram B. Baliga

## Examples

``` r
## One input
deg_2_rad(90)
#> [1] 1.570796

## Multiple inputs
deg_2_rad(c(5, 10, 15, 20))
#> [1] 0.08726646 0.17453293 0.26179939 0.34906585
```
