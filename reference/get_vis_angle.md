# Estimate visual angles from a subject's perspective in an experimental tunnel

Estimate visual angles from a subject's perspective in an experimental
tunnel

## Usage

``` r
get_vis_angle(obj_name)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attributes
  `pathviewr_steps` that include `"viewr"` and `min_dist_calculated`.

## Value

A tibble or data.frame with added variables for `vis_angle_pos_rad`,
`vis_angle_pos_deg`, `vis_angle_neg_rad`, `vos_angle_neg_deg`,
`vis_angle_end_rad`, and `vis_angle_end_deg`.

## Details

`get_vis_angle()` assumes the following:

- The subject's gaze is fixed at the point on the either side of the
  tunnel that minimizes the distance to visual stimuli and therefore
  maximizes visual angles.

- The subject's head is facing parallel to the length axis of the
  tunnel. Visual perception functions in future versions of pathviewr
  will integrate head orientation coordinates. Angles are reported in
  radians/cycle (`vis_angle_pos_rad`) and degrees/cycle
  (`vis_angle_pos_deg`).

## See also

Other visual perception functions:
[`calc_min_dist_box()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_box.md),
[`get_sf()`](https://docs.ropensci.org/pathviewr/reference/get_sf.md)

## Author

Eric R. Press

## Examples

``` r
 ## Import sample data from package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                              package = 'pathviewr'))
flydra_data <-
  read_flydra_mat(system.file("extdata", "pathviewr_flydra_example_data.mat",
                              package = 'pathviewr'),
                              subject_name = "birdie_sanders")

 ## Process data up to and including get_min_dist()
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
  calc_min_dist_v(simplify_output = TRUE) %>%

  ## Now calculate the visual angles
  get_vis_angle()
#> autodetect is an experimental feature -- please report issues.

  flydra_data_full <-
  flydra_data %>%
  redefine_tunnel_center(length_method = "middle",
                        height_method = "user-defined",
                        height_zero = 1.44) %>%
  select_x_percent(desired_percent = 50) %>%
  separate_trajectories(max_frame_gap = "autodetect") %>%
  get_full_trajectories(span = 0.95) %>%
  insert_treatments(tunnel_config = "box",
                   tunnel_length = 3,
                   tunnel_width = 1,
                   stim_param_lat_pos = 0.1,
                   stim_param_lat_neg = 0.1,
                   stim_param_end_pos = 0.3,
                   stim_param_end_neg = 0.3,
                   treatment = "lat10_end_30") %>%
  calc_min_dist_box() %>%

   ## Now calculate the visual angles
  get_vis_angle()
#> autodetect is an experimental feature -- please report issues.
```
