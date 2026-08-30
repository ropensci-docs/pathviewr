# Compute distance between a point and a line

Compute distance between a point and a line

## Usage

``` r
get_dist_point_line(point, line_coord1, line_coord2)
```

## Arguments

- point:

  2D or 3D coordinates of the point as c(x,y) or c(x,y,z)

- line_coord1:

  2D or 3D coordinates of one point on the line as c(x,y) or c(x,y,z)

- line_coord2:

  2D or 3D coordinates of a second point on the line as c(x,y) or
  c(x,y,z)

## Value

A numeric vector of length 1 that provides the euclidean distance
between the point and the line.

## Details

The function accepts 2D coordinates or 3D coordinates, but note that the
dimensions of all supplied arguments must match; all coordinates must be
2D or they all must be 3D.

## See also

Other mathematical functions:
[`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md),
[`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
[`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md),
[`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md),
[`get_3d_cross_prod()`](https://docs.ropensci.org/pathviewr/reference/get_3d_cross_prod.md),
[`get_traj_velocities()`](https://docs.ropensci.org/pathviewr/reference/get_traj_velocities.md),
[`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md),
[`rad_2_deg()`](https://docs.ropensci.org/pathviewr/reference/rad_2_deg.md)

## Author

Vikram B. Baliga

## Examples

``` r
## 2D case
get_dist_point_line(
  point = c(0, 0),
  line_coord1 = c(1, 0),
  line_coord2 = c(1, 5)
)
#> [1] 1

## 3D case
get_dist_point_line(
  point = c(0, 0, 0),
  line_coord1 = c(1, 0, 0),
  line_coord2 = c(1, 5, 0)
)
#> [1] 1
```
