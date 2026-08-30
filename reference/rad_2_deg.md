# Convert radians to degrees

Convert radians to degrees

## Usage

``` r
rad_2_deg(rad)
```

## Arguments

- rad:

  Radians (a numeric of any length \>= 1)

## Value

The angle(s) in degrees (as a numeric vector of the same length)

## See also

Other mathematical functions:
[`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md),
[`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
[`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md),
[`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md),
[`get_3d_cross_prod()`](https://docs.ropensci.org/pathviewr/reference/get_3d_cross_prod.md),
[`get_dist_point_line()`](https://docs.ropensci.org/pathviewr/reference/get_dist_point_line.md),
[`get_traj_velocities()`](https://docs.ropensci.org/pathviewr/reference/get_traj_velocities.md),
[`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md)

## Author

Vikram B. Baliga

## Examples

``` r
## One input
rad_2_deg(pi/2)
#> [1] 90

## Multiple inputs
rad_2_deg(c(pi / 2, pi, 2 * pi))
#> [1]  90 180 360
```
