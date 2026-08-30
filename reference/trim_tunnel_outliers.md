# Trim out artifacts and other outliers from the extremes of the tunnel

The user provides estimates of min and max values of data. This function
then trims out anything beyond these estimates.

## Usage

``` r
trim_tunnel_outliers(
  obj_name,
  lengths_min = 0,
  lengths_max = 3,
  widths_min = -0.4,
  widths_max = 0.8,
  heights_min = -0.2,
  heights_max = 0.5,
  ...
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"` that has been passed through
  [`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md)
  and
  [`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md)
  (or is structured as though it has been passed through those
  functions).

- lengths_min:

  Minimum length

- lengths_max:

  Maximum length

- widths_min:

  Minimum width

- widths_max:

  Maximum width

- heights_min:

  Minimum height

- heights_max:

  Maximum height

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) in which data outside the specified ranges has
been excluded.

## Details

Anything supplied to \_min or \_max arguments should be single numeric
values.

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
## "gather" step before running trim_tunnel_outliers().
motive_gathered <-
  motive_data %>%
  relabel_viewr_axes() %>%
  gather_tunnel_data()

## Now trim outliers using default values
motive_trimmed <-
  motive_gathered %>%
  trim_tunnel_outliers(lengths_min = 0,
                       lengths_max = 3,
                       widths_min = -0.4,
                       widths_max = 0.8,
                       heights_min = -0.2,
                       heights_max = 0.5)
```
