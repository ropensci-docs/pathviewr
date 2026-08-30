# Redefine frames and time stamps on a per-trajectory basis

After a data set has been separated into trajectories, find the earliest
frame in each trajectory and set the corresponding time to 0. All
subsequent time_sec stamps are computed according to successive frame
numbering.

## Usage

``` r
set_traj_frametime(obj_name)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`.
New columns include traj_time (the trajectory-specific time values) and
traj_frame (the trajectory-specific frame numbering).

## Details

The separate_trajectories() and get_full_trajectories() must be run
prior to use. The initial traj_time and traj_frame values are set to 0
within each trajectory.

## See also

Other utility functions:
[`clean_by_span()`](https://docs.ropensci.org/pathviewr/reference/clean_by_span.md),
[`insert_treatments()`](https://docs.ropensci.org/pathviewr/reference/insert_treatments.md),
[`remove_duplicate_frames()`](https://docs.ropensci.org/pathviewr/reference/remove_duplicate_frames.md),
[`remove_vel_anomalies()`](https://docs.ropensci.org/pathviewr/reference/remove_vel_anomalies.md)

## Author

Vikram B. Baliga
