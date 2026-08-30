# Retain trajectories that span a selected region of interest

Specify a minimum span of the selected region of interest and then keep
trajectories that are wider than that span and go from one end to the
other of the region.

## Usage

``` r
get_full_trajectories(obj_name, span = 0.8, ...)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- span:

  Span to use; must be numeric and between 0 and 1

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) in which only trajectories that span the region
of interest are retained. Data are labeled by direction (either
"leftwards" or "rightwards") with respect to their starting and ending
`position_length` values in the `direction` column.

## Details

Because trajectories may not have observations exactly at the beginning
or the end of the region of interest, it may be necessary to allow
trajectories to be slightly shorter than the range of the selected
region of interest. The `span` parameter of this function handles this.
By supplying a numeric proportion from 0 to 1, a user may allow
trajectories to span that proportion of the selected region. For
example, setting `span = 0.95` will keep all trajectories that span 95%
of the length of the selected region of interest. Setting `span = 1`
(not recommended) will strictly keep trajectories that start and end at
the exact cut-offs of the selected region of interest. For these
reasons, `span`s of 0.99 to 0.95 are generally recommended.

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
[`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

Other functions that define or clean trajectories:
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

## Author

Vikram B. Baliga

## Examples

``` r
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                              package = 'pathviewr'))

## Clean the file. It is generally recommended to clean up to the
## "separate" step before running select_x_percent().
motive_separated <-
  motive_data %>%
  relabel_viewr_axes() %>%
  gather_tunnel_data() %>%
  trim_tunnel_outliers() %>%
  rotate_tunnel() %>%
  select_x_percent(desired_percent = 50) %>%
  separate_trajectories(max_frame_gap = "autodetect",
                        frame_rate_proportion = 0.1)
#> autodetect is an experimental feature -- please report issues.

## Now retain only the "full" trajectories that span
## across 0.95 of the range of position_length
motive_full <-
  motive_separated %>%
  get_full_trajectories(span = 0.95)
```
