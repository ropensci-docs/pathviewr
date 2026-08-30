# Compute the cross product of two 3D vectors

Compute the cross product of two 3D vectors

## Usage

``` r
get_3d_cross_prod(v1, v2)
```

## Arguments

- v1:

  First vector, as c(x,y,z)

- v2:

  Second vector, as c(x,y,z)

## Value

A vector of length 3 that describes the cross-product

## See also

Other mathematical functions:
[`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md),
[`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
[`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md),
[`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md),
[`get_dist_point_line()`](https://docs.ropensci.org/pathviewr/reference/get_dist_point_line.md),
[`get_traj_velocities()`](https://docs.ropensci.org/pathviewr/reference/get_traj_velocities.md),
[`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md),
[`rad_2_deg()`](https://docs.ropensci.org/pathviewr/reference/rad_2_deg.md)

## Author

Vikram B. Baliga

## Examples

``` r
v1 <- c(1, 1, 3)
v2 <- c(3, 1, 3)
get_3d_cross_prod(v1, v2)
#> [1]  0  6 -2
```
