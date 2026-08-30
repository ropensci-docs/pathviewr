# Separate rows of data into separately labeled trajectories.

Separate rows of data into separately labeled trajectories.

## Usage

``` r
separate_trajectories(
  obj_name,
  max_frame_gap = 1,
  frame_rate_proportion = 0.1,
  frame_gap_messaging = FALSE,
  frame_gap_plotting = FALSE,
  ...
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- max_frame_gap:

  Default 1; defines the largest permissible gap in data before a new
  trajectory is forced to be defined. Can be either a numeric value or
  "autodetect". See Details for more.

- frame_rate_proportion:

  Default 0.10; if `max_frame_gap = "autodetect"`, proportion of frame
  rate to be used as a reference (see Details).

- frame_gap_messaging:

  Default FALSE; should frame gaps be reported in the console?

- frame_gap_plotting:

  Default FALSE; should frame gap diagnostic plots be shown?

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) in which a new column `file_sub_traj` is added,
which labels trajectories within the data by concatenating file name,
subject name, and a trajectory number (all separated by underscores).

## Details

This function is designed to separate rows of data into separately
labeled trajectories.

The `max_frame_gap` parameter determines how trajectories will be
separated. If numeric, the function uses the supplied value as the
largest permissible gap in frames before a new trajectory is defined.

If `max_frame_gap = "autodetect"` is used, the function attempts to
guesstimate the best value(s) of `max_frame_gap`. This is performed
separately for each subject in the data set, i.e. as many
`max_frame_gap` values will be estimated as there are unique subjects.
The highest possible value of any `max_frame_gap` is first set as a
proportion of the capture frame rate, as defined by the
`frame_rate_proportion` parameter (default 0.10). For each subject, a
plot of total trajectory counts vs. max frame gap values is created
internally (but can be plotted via setting `frame_gap_plotting = TRUE`).
As larger max frame gaps are allowed, trajectory count will necessarily
decrease but may reach a value that likely represents the "best" option.
The "elbow" of that plot is then used to find an estimate of the best
max frame gap value to use.

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
[`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

Other functions that define or clean trajectories:
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

## Author

Vikram B. Baliga and Melissa S. Armstrong

## Examples

``` r
## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                              package = 'pathviewr'))

## Clean the file. It is generally recommended to clean up to the
## "select" step before running select_x_percent().
motive_selected <-
  motive_data %>%
  relabel_viewr_axes() %>%
  gather_tunnel_data() %>%
  trim_tunnel_outliers() %>%
  rotate_tunnel() %>%
  select_x_percent(desired_percent = 50)

## Now separate trajectories using autodetect
motive_separated <-
  motive_selected %>%
  separate_trajectories(max_frame_gap = "autodetect",
                        frame_rate_proportion = 0.1)
#> autodetect is an experimental feature -- please report issues.

## See new column file_sub_traj for trajectory labeling
names(motive_separated)
#>  [1] "frame"             "time_sec"          "subject"          
#>  [4] "position_length"   "position_width"    "position_height"  
#>  [7] "rotation_length"   "rotation_width"    "rotation_height"  
#> [10] "rotation_real"     "mean_marker_error" "traj_id"          
#> [13] "file_sub_traj"    
```
