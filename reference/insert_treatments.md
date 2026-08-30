# Inserts treatment and experiment information

Adds information about treatment and experimental set up to viewr
objects for analysis in other pathviewr functions

## Usage

``` r
insert_treatments(
  obj_name,
  tunnel_config = "box",
  perch_2_vertex = NULL,
  vertex_angle = NULL,
  tunnel_width = NULL,
  tunnel_length = NULL,
  stim_param_lat_pos = NULL,
  stim_param_lat_neg = NULL,
  stim_param_end_pos = NULL,
  stim_param_end_neg = NULL,
  treatment = NULL
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- tunnel_config:

  The configuration of the experimental tunnel. Currently, pathviewr
  supports rectangular "box" and V-shaped tunnel configurations.

- perch_2_vertex:

  If using a V-shaped tunnel, this is the vertical distance between the
  vertex and the height of the perches. If the tunnel does not have
  perches, insert the vertical distance between the vertex and the
  height of the origin (0,0,0).

- vertex_angle:

  If using a V-shaped tunnel, the angle of the vertex (in degrees)
  `vertex_angle` defaults to 90.

- tunnel_width:

  If using a box-shaped tunnel, the width of the tunnel.

- tunnel_length:

  The length of the tunnel.

- stim_param_lat_pos:

  The size of the stimulus on the lateral positive wall of the tunnel.
  Eg. for 10cm wide gratings, `stim_param_lat_pos` = 0.1.

- stim_param_lat_neg:

  The size of the stimulus on the lateral negative wall of the tunnel..

- stim_param_end_pos:

  The size of the stimulus on the end positive wall of the tunnel.

- stim_param_end_neg:

  The size of the stimulus on the end negative wall of the tunnel.

- treatment:

  The name of the treatment assigned to all rows of the viewr object.
  Currently only able to accept a single treatment per viewr data
  object.

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"treatments added"`). Depending on the argument
`tunnel_config`, the viewr object also includes columns storing the
values of the supplied arguments. This experimental information is also
stored in the viewr object's metadata

## Details

All length measurements reported in meters.

## See also

Other utility functions:
[`clean_by_span()`](https://docs.ropensci.org/pathviewr/reference/clean_by_span.md),
[`remove_duplicate_frames()`](https://docs.ropensci.org/pathviewr/reference/remove_duplicate_frames.md),
[`remove_vel_anomalies()`](https://docs.ropensci.org/pathviewr/reference/remove_vel_anomalies.md),
[`set_traj_frametime()`](https://docs.ropensci.org/pathviewr/reference/set_traj_frametime.md)

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

  ## Clean data up to and including get_full_trajectories()
motive_data_full <-
 motive_data %>%
 relabel_viewr_axes() %>%
 gather_tunnel_data() %>%
 trim_tunnel_outliers() %>%
 rotate_tunnel() %>%
 select_x_percent(desired_percent = 50) %>%
 separate_trajectories(max_frame_gap = "autodetect") %>%
 get_full_trajectories(span = 0.95)
#> autodetect is an experimental feature -- please report issues.

 flydra_data_full <-
  flydra_data %>%
  redefine_tunnel_center(length_method = "middle",
                        height_method = "user-defined",
                        height_zero = 1.44) %>%
  select_x_percent(desired_percent = 50) %>%
  separate_trajectories(max_frame_gap = "autodetect") %>%
  get_full_trajectories(span = 0.95)
#> autodetect is an experimental feature -- please report issues.


## Now add information about the experimental configuration. In this example,
## a V-shaped tunnel in which the vertex is 90deg and lies 0.40m below the
## origin. The visual stimuli on the lateral and end walls have a cycle
## length of 0.1m and 0.3m respectively, and the treatment is labeled
## "lat10_end30"

motive_v <-
motive_data_full %>%
 insert_treatments(tunnel_config = "v",
                   perch_2_vertex = 0.4,
                   vertex_angle = 90,
                   tunnel_length = 2,
                   stim_param_lat_pos = 0.1,
                   stim_param_lat_neg = 0.1,
                   stim_param_end_pos = 0.3,
                   stim_param_end_neg = 0.3,
                   treatment = "lat10_end_30")

# For an experiment using the box-shaped configuration where the tunnel is 1m
# wide and 3m long and the visual stimuli on the lateral and end walls have a
# cycle length of 0.2 and 0.3m, respectively, and the treatment is labeled
# "lat20_end30".

flydra_box <-
 flydra_data_full %>%
 insert_treatments(tunnel_config = "box",
                   tunnel_width = 1,
                   tunnel_length = 3,
                   stim_param_lat_pos = 0.2,
                   stim_param_lat_neg = 0.2,
                   stim_param_end_pos = 0.3,
                   stim_param_end_neg = 0.3,
                   treatment = "lat20_end30")

## Check out the new columns in the resulting objects
names(motive_v)
#>  [1] "tunnel_config"      "perch_2_vertex"     "vertex_angle"      
#>  [4] "tunnel_length"      "stim_param_lat_pos" "stim_param_lat_neg"
#>  [7] "stim_param_end_pos" "stim_param_end_neg" "treatment"         
#> [10] "frame"              "time_sec"           "subject"           
#> [13] "position_length"    "position_width"     "position_height"   
#> [16] "rotation_length"    "rotation_width"     "rotation_height"   
#> [19] "rotation_real"      "mean_marker_error"  "traj_id"           
#> [22] "file_sub_traj"      "traj_length"        "start_length"      
#> [25] "end_length"         "length_diff"        "start_length_sign" 
#> [28] "end_length_sign"    "direction"         
names(flydra_box)
#>  [1] "tunnel_config"      "tunnel_width"       "tunnel_length"     
#>  [4] "stim_param_lat_pos" "stim_param_lat_neg" "stim_param_end_pos"
#>  [7] "stim_param_end_neg" "treatment"          "frame"             
#> [10] "time_sec"           "subject"            "position_length"   
#> [13] "position_width"     "position_height"    "velocity"          
#> [16] "length_inst_vel"    "width_inst_vel"     "height_inst_vel"   
#> [19] "traj_id"            "file_sub_traj"      "traj_length"       
#> [22] "start_length"       "end_length"         "length_diff"       
#> [25] "start_length_sign"  "end_length_sign"    "direction"         
```
