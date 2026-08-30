# Remove any duplicates or aliased frames within trajectories

Remove any duplicates or aliased frames within trajectories

## Usage

``` r
remove_duplicate_frames(obj_name)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`.

## Details

The separate_trajectories() and get_full_trajectories() must be run
prior to use.

## See also

Other utility functions:
[`clean_by_span()`](https://docs.ropensci.org/pathviewr/reference/clean_by_span.md),
[`insert_treatments()`](https://docs.ropensci.org/pathviewr/reference/insert_treatments.md),
[`remove_vel_anomalies()`](https://docs.ropensci.org/pathviewr/reference/remove_vel_anomalies.md),
[`set_traj_frametime()`](https://docs.ropensci.org/pathviewr/reference/set_traj_frametime.md)

## Author

Vikram B. Baliga
