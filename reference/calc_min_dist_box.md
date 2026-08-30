# Calculate minimum distance to lateral and end walls in a box-shaped experimental tunnel

Calculate minimum distance to lateral and end walls in a box-shaped
experimental tunnel

## Usage

``` r
calc_min_dist_box(obj_name)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that include `"viewr"` and `treatments_added`.

## Value

A tibble or data.frame with added variables for `min_dist_pos`,
`min_dist_neg`, and `min_dist_end`,.

## Details

`calc_min_dist_box()` assumes the subject locomotes facing forward,
therefore `min_dist_end` represents the minimum distance between the
subject and the end wall to which it is moving towards. All outputs are
in meters.

## See also

Other visual perception functions:
[`get_sf()`](https://docs.ropensci.org/pathviewr/reference/get_sf.md),
[`get_vis_angle()`](https://docs.ropensci.org/pathviewr/reference/get_vis_angle.md)

## Author

Eric R. Press

## Examples

``` r
## Import sample data from package
 flydra_data <-
 read_flydra_mat(system.file("extdata", "pathviewr_flydra_example_data.mat",
                               package = 'pathviewr'),
                               subject_name = "birdie_sanders")

   ## Process data up to and including insert_treatments()
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

   ## Now calculate the minimum distances to each wall
   calc_min_dist_box()
#> autodetect is an experimental feature -- please report issues.

   ## See 3 new variables for calculations to lateral and end walls
   names(flydra_data_full)
#>  [1] "tunnel_config"      "tunnel_width"       "tunnel_length"     
#>  [4] "stim_param_lat_pos" "stim_param_lat_neg" "stim_param_end_pos"
#>  [7] "stim_param_end_neg" "treatment"          "frame"             
#> [10] "time_sec"           "subject"            "position_length"   
#> [13] "position_width"     "position_height"    "velocity"          
#> [16] "length_inst_vel"    "width_inst_vel"     "height_inst_vel"   
#> [19] "traj_id"            "file_sub_traj"      "traj_length"       
#> [22] "start_length"       "end_length"         "length_diff"       
#> [25] "start_length_sign"  "end_length_sign"    "direction"         
#> [28] "min_dist_pos"       "min_dist_neg"       "min_dist_end"      
```
