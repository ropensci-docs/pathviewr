# Calculate minimum distance to lateral and end walls in a V-shaped experimental tunnel

Calculate minimum distance to lateral and end walls in a V-shaped
experimental tunnel

## Usage

``` r
calc_min_dist_v(obj_name, simplify_output = TRUE)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"` and `treatments_added`.

- simplify_output:

  If TRUE, the returned object includes only the minimum distance
  between the subject and the lateral/end walls. If FALSE, the returned
  object includes all variables internal to the calculation.

## Value

A tibble or data.frame with added variables for `height_2_vertex`,
`height_2_screen`, `width_2_screen_pos`, `width_2_screen_neg`,
`min_dist_pos`, `min_dist_neg`, `min_dist_end`, `bound_pos`, and
`bound_neg`.

## Details

For tunnels in which `vertex_angle` is \>90 degree, `bound_pos` and
`bound_neg` represent a planes orthogonal to the lateral walls and are
used to modify `min_dist_pos` and `min_dist_neg` calculations to prevent
erroneous outputs. `calc_min_dist_v()` assumes the subject locomotes
facing forward, therefore `min_dist_end` represents the minimum distance
between the subject and the end wall to which it is moving towards All
outputs are in meters.

## See also

Other mathematical functions:
[`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md),
[`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md),
[`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md),
[`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md),
[`get_3d_cross_prod()`](https://docs.ropensci.org/pathviewr/reference/get_3d_cross_prod.md),
[`get_dist_point_line()`](https://docs.ropensci.org/pathviewr/reference/get_dist_point_line.md),
[`get_traj_velocities()`](https://docs.ropensci.org/pathviewr/reference/get_traj_velocities.md),
[`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md),
[`rad_2_deg()`](https://docs.ropensci.org/pathviewr/reference/rad_2_deg.md)

## Author

Eric R. Press

## Examples

``` r
 ## Import sample data from package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                              package = 'pathviewr'))

 ## Process data up to and including insert_treatments()
motive_data_full <-
  motive_data %>%
  relabel_viewr_axes() %>%
  gather_tunnel_data() %>%
  trim_tunnel_outliers() %>%
  rotate_tunnel() %>%
  select_x_percent(desired_percent = 50) %>%
  separate_trajectories(max_frame_gap = "autodetect") %>%
  get_full_trajectories(span = 0.95) %>%
  insert_treatments(tunnel_config = "v",
                   perch_2_vertex = 0.4,
                   vertex_angle = 90,
                   tunnel_length = 2,
                   stim_param_lat_pos = 0.1,
                   stim_param_lat_neg = 0.1,
                   stim_param_end_pos = 0.3,
                   stim_param_end_neg = 0.3,
                   treatment = "lat10_end_30") %>%

 ## Now calculate the minimum distances to each wall
  calc_min_dist_v(simplify_output = TRUE)
#> autodetect is an experimental feature -- please report issues.

  ## See 3 new variables for calculations to lateral and end walls
  names(motive_data_full)
#>  [1] "tunnel_config"      "perch_2_vertex"     "vertex_angle"      
#>  [4] "tunnel_length"      "stim_param_lat_pos" "stim_param_lat_neg"
#>  [7] "stim_param_end_pos" "stim_param_end_neg" "treatment"         
#> [10] "frame"              "time_sec"           "subject"           
#> [13] "position_length"    "position_width"     "position_height"   
#> [16] "rotation_length"    "rotation_width"     "rotation_height"   
#> [19] "rotation_real"      "mean_marker_error"  "traj_id"           
#> [22] "file_sub_traj"      "traj_length"        "start_length"      
#> [25] "end_length"         "length_diff"        "start_length_sign" 
#> [28] "end_length_sign"    "direction"          "min_dist_pos"      
#> [31] "min_dist_neg"       "min_dist_end"      
```
