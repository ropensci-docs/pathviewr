# Estimate the spatial frequency of visual stimuli from the subject's perspective in an experimental tunnel.

Estimate the spatial frequency of visual stimuli from the subject's
perspective in an experimental tunnel.

## Usage

``` r
get_sf(obj_name)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"` and `vis_angles_calculated`.

## Value

A tibble or data.frame with added variables for `sf_pos`, `sf_neg`, and
`sf_end`. angle.

## Details

`get_sf()` assumes the following:

- The subject's gaze is fixed at the point on the either side of the
  tunnel that minimizes the distance to visual stimuli and therefore
  maximizes visual angles.

- The subject's head is facing parallel to the length axis of the
  tunnel. Visual perception functions in future versions of pathviewr
  will integrate head orientation coordinates. Spatial frequency is
  reported in cycles/degree and is the inverse of visual angle
  (degrees/cycle).

## See also

Other visual perception functions:
[`calc_min_dist_box()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_box.md),
[`get_vis_angle()`](https://docs.ropensci.org/pathviewr/reference/get_vis_angle.md)

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

 ## Process data up to and including get_vis_angle()
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
  get_vis_angle() %>%

  ## Now calculate the spatial frequencies
  get_sf()
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
  get_vis_angle() %>%

  ## Now calculate the spatial frequencies
  get_sf()
#> autodetect is an experimental feature -- please report issues.
```
