# Remove trajectories entirely, based on velocity thresholds

Remove trajectories from a viewr object that contain instances of
velocity known to be spurious.

## Usage

``` r
exclude_by_velocity(obj_name, vel_min = NULL, vel_max = NULL)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`

- vel_min:

  Default `NULL`. If a numeric is entered, trajectories that have at
  least one observation with velocity less than `vel_min` are removed.

- vel_max:

  Default `NULL`. If a numeric is entered, trajectories that have at
  least one observation with velocity greater than `vel_max` are
  removed.

## Value

A new viewr object that is identical to the input object but now
excludes any trajectories that contain observations with velocity less
than `vel_min` (if specified) and/or velocity greater than `vel_max` (if
specified)

## Author

Vikram B. Baliga

## Examples

``` r
## Import and clean the example Motive data
motive_import_and_clean <-
  import_and_clean_viewr(
    file_name = system.file("extdata", "pathviewr_motive_example_data.csv",
                            package = 'pathviewr'),
    desired_percent = 50,
    max_frame_gap = "autodetect",
    span = 0.95
  )
#> autodetect is an experimental feature -- please report issues.

## See the distribution of velocities
hist(motive_import_and_clean$velocity)


## Let's remove any trajectories that contain
## velocity < 2
motive_vel_filtered <-
  motive_import_and_clean %>%
  exclude_by_velocity(vel_min = 2)

## See how the distribution of velocities has changed
hist(motive_vel_filtered$velocity)
```
