# Compute an angle in 2D space

Compute an angle in 2D space

## Usage

``` r
get_2d_angle(x1, y1, x2, y2, x3, y3)
```

## Arguments

- x1:

  x-coordinate of first point

- y1:

  y-coordinate of first point

- x2:

  x-coordinate of second point (vertex)

- y2:

  y-coordinate of second point (vertex)

- x3:

  x-coordinate of third point

- y3:

  y-coordinate of third point

## Value

A numeric vector that provides the angular measurement in degrees.

## Details

Everything supplied to arguments must be numeric values or vectors of
numeric values. The second point (x2, y2) is treated as the vertex, and
the angle between the three points in 2D space is computed.

## See also

Other mathematical functions:
[`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md),
[`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
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
get_2d_angle(
  0, 1,
  0, 0,
  1, 0)
#> [1] 90
```
