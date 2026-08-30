# Rename subjects in the data via pattern detection

Quick utility function to use str_replace with mutate(across()) to
batch- rename subjects via pattern detection.

## Usage

``` r
rename_viewr_characters(
  obj_name,
  target_column = "subject",
  pattern,
  replacement = ""
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- target_column:

  The target column; defaults to "subject"

- pattern:

  The (regex) pattern to be replaced

- replacement:

  The replacement text. Must be a character

## Value

A tibble or data frame in which subjects have been renamed according to
the `pattern` and `replacement` supplied by the user.

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

## Author

Vikram B. Baliga

## Examples

``` r
## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

## Clean the file. It is generally recommended to clean up to the
## "gather" step before running rescale_tunnel_data().
 motive_gathered <-
   motive_data %>%
   relabel_viewr_axes() %>%
   gather_tunnel_data()

## See the subject names
 unique(motive_gathered$subject)
#> [1] "device02" "device03" "device05"

## Now rename the subjects. We'll get rid of "device" and replace it
## with "subject"
motive_renamed <-
  motive_gathered %>%
  rename_viewr_characters(target_column = "subject",
                          pattern = "device",
                          replacement = "subject")
#> Warning: There was 1 warning in `dplyr::mutate()`.
#> ℹ In argument: `dplyr::across(...)`.
#> Caused by warning:
#> ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
#> Supply arguments directly to `.fns` through an anonymous function instead.
#> 
#>   # Previously
#>   across(a:b, mean, na.rm = TRUE)
#> 
#>   # Now
#>   across(a:b, \(x) mean(x, na.rm = TRUE))
#> ℹ The deprecated feature was likely used in the pathviewr package.
#>   Please report the issue at <https://github.com/ropensci/pathviewr/issues/>.

## See the new subject names
unique(motive_renamed$subject)
#> [1] "subject02" "subject03" "subject05"
```
