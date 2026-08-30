# Remove any rows which show sharp shifts in velocity that are likely due to tracking errors

Remove any rows which show sharp shifts in velocity that are likely due
to tracking errors

## Usage

``` r
remove_vel_anomalies(
  obj_name,
  target = "velocity",
  method = "gesd",
  alpha = 0.05,
  max_anoms = 0.2
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- target:

  The column to target; defaults to "velocity"

- method:

  The anomaly detection method; see anomalize::anomalize()

- alpha:

  The width of the "normal" range; see anomalize::anomalize()

- max_anoms:

  The max proportion of anomalies; see anomalize::anomalize()

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`.
Rows in which large anomalies were detected have been removed. No
additional columns are created.

## Details

This function runs anomalize::anomalize() on a per-trajectory basis. The
separate_trajectories() and get_full_trajectories() must be run prior to
use.

## See also

Other utility functions:
[`clean_by_span()`](https://docs.ropensci.org/pathviewr/reference/clean_by_span.md),
[`insert_treatments()`](https://docs.ropensci.org/pathviewr/reference/insert_treatments.md),
[`remove_duplicate_frames()`](https://docs.ropensci.org/pathviewr/reference/remove_duplicate_frames.md),
[`set_traj_frametime()`](https://docs.ropensci.org/pathviewr/reference/set_traj_frametime.md)

## Author

Vikram B. Baliga
