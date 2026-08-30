# Visualize the consequence of using various max_frame_gap values

Run separate_trajectories() with many different frame gaps to help
determine what value to use

## Usage

``` r
visualize_frame_gap_choice(obj_name, loops = 20, ...)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- loops:

  How many total frame gap entries to consider. Each loop will increase
  the `max_fram_gap` argument in `separate_trajectories` by 1.

- ...:

  Additional arguments

## Value

A plot and a tibble, each of which shows the total number of
trajectories that result from using the specified range of
`max_frame_gap` values.

## Details

The input viewr object (`obj_name`) should likely be an object that has
passed through the
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md)
step.

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
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md)

Other plotting functions:
[`plot_by_subject()`](https://docs.ropensci.org/pathviewr/reference/plot_by_subject.md),
[`plot_viewr_trajectories()`](https://docs.ropensci.org/pathviewr/reference/plot_viewr_trajectories.md)

Other functions that define or clean trajectories:
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md)

## Author

Melissa S. Armstrong and Vikram B. Baliga

## Examples

``` r
library(pathviewr)

## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

motive_selected <-
  motive_data %>%
  relabel_viewr_axes() %>%
  gather_tunnel_data() %>%
  trim_tunnel_outliers() %>%
  rotate_tunnel() %>%
  get_velocity() %>%
  select_x_percent(desired_percent = 50)

visualize_frame_gap_choice(motive_selected, loops = 10)

#> [[1]]
#> # A tibble: 10 × 3
#>    frame_gap_allowed trajectory_count file_id        
#>                <dbl>            <dbl> <chr>          
#>  1                 1               15 motive_selected
#>  2                 2               13 motive_selected
#>  3                 3               13 motive_selected
#>  4                 4               13 motive_selected
#>  5                 5               13 motive_selected
#>  6                 6               13 motive_selected
#>  7                 7               13 motive_selected
#>  8                 8               13 motive_selected
#>  9                 9               13 motive_selected
#> 10                10               13 motive_selected
#> 
#> [[2]]
#> NULL
#> 
```
