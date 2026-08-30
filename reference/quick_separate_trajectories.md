# Quick version of separate_trajectories()

Mostly meant for internal use but available nevertheless.

## Usage

``` r
quick_separate_trajectories(obj_name, max_frame_gap = 1, ...)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- max_frame_gap:

  Unlike the corresponding parameter in `separate_trajectories`, must be
  a single numeric here.

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
separated. `max_frame_gap` defines the largest permissible gap in data
before a new trajectory is forced to be defined. In this function, only
a single numeric can be supplied to this parameter (unlike the case in
`separate_trajectories`).

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
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
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

## Author

Vikram B. Baliga

## Examples

``` r
## This function is not recommended for general use.
## See separate_trajectories() instead
```
