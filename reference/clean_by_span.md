# Remove file_sub_traj entries that do not span the full region of interest

Remove file_sub_traj entries that do not span the full region of
interest

## Usage

``` r
clean_by_span(
  obj_name,
  axis = "position_length",
  min_value = NULL,
  max_value = NULL,
  tolerance = 0.1
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- axis:

  Along which axis should restrictions be enforced?

- min_value:

  Minimum coordinate value; setting this to NULL will auto-compute the
  best value

- max_value:

  Maximum coordinate; setting this to NULL will auto-compute the best
  value

- tolerance:

  As a proporiton of axis value

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`.
Trajectories that do not span the full region of interest have been
removed; trajectory identities (file_sub_traj) have not been changed.

## See also

Other utility functions:
[`insert_treatments()`](https://docs.ropensci.org/pathviewr/reference/insert_treatments.md),
[`remove_duplicate_frames()`](https://docs.ropensci.org/pathviewr/reference/remove_duplicate_frames.md),
[`remove_vel_anomalies()`](https://docs.ropensci.org/pathviewr/reference/remove_vel_anomalies.md),
[`set_traj_frametime()`](https://docs.ropensci.org/pathviewr/reference/set_traj_frametime.md)

## Author

Vikram B. Baliga
