# Convert data from another format into a viewr object

Should you have data from a non-Motive, non-Flydra source, this function
can be used to ensure your data are put into the right format to work
with other pathviewr functions.

## Usage

``` r
as_viewr(
  obj_name,
  frame_rate = 100,
  frame_col,
  time_col,
  subject_col,
  position_length_col,
  position_width_col,
  position_height_col,
  include_rotation = FALSE,
  rotation_real_col,
  rotation_length_col,
  rotation_width_col,
  rotation_height_col
)
```

## Arguments

- obj_name:

  A tibble or data frame containing movement trajectories

- frame_rate:

  Must be a single numeric value indicating capture frame rate in frames
  per second.

- frame_col:

  Column number of obj_name that contains frame numbers

- time_col:

  Column number of obj_name that contains time (must be in seconds)

- subject_col:

  Column number of obj_name that contains subject name(s)

- position_length_col:

  Column number of obj_name that contains length-axis position values

- position_width_col:

  Column number of obj_name that contains width-axis position values

- position_height_col:

  Column number of obj_name that contains height-axis position values

- include_rotation:

  Are rotation data included? Defaults to FALSE

- rotation_real_col:

  Column number of obj_name that contains the "real" axis of quaternion
  rotation data

- rotation_length_col:

  Column number of obj_name that contains the length axis of quaternion
  rotation data

- rotation_width_col:

  Column number of obj_name that contains the width axis of quaternion
  rotation data

- rotation_height_col:

  Column number of obj_name that contains the height axis of quaternion
  rotation data

## Value

A tibble that is organized to be compliant with other `pathviewr`
functions and that contains the attributes `pathviewr_steps` with
entries set to `c("viewr", "renamed_tunnel", "gathered_tunnel")`

## See also

Other data import functions:
[`import_and_clean_batch()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_batch.md),
[`import_batch()`](https://docs.ropensci.org/pathviewr/reference/import_batch.md),
[`read_flydra_mat()`](https://docs.ropensci.org/pathviewr/reference/read_flydra_mat.md),
[`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)

## Author

Vikram B. Baliga

## Examples

``` r

## Create a dummy data frame with simulated (nonsense) data
df <- data.frame(frame = seq(1, 100, by = 1),
                 time_sec = seq(0, by = 0.01, length.out = 100),
                 subject = "birdie_sanders",
                 z = rnorm(100),
                 x = rnorm(100),
                 y = rnorm(100))

## Use as_viewr() to convert it into a viewr object
test <-
  as_viewr(
    df,
    frame_rate = 100,
    frame_col = 1,
    time_col = 2,
    subject_col = 3,
    position_length_col = 5,
    position_width_col = 6,
    position_height_col = 4
  )
```
