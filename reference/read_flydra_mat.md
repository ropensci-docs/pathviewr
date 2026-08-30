# Import data from a MAT file exported from Flydra software

`read_flydra_mat()` is designed to import data from a `.mat` file that
has been exported from Flydra software. The resultant object is a tibble
that additionally has important metadata stored as attributes (see
Details).

## Usage

``` r
read_flydra_mat(mat_file, file_id = NA, subject_name, frame_rate = 100, ...)
```

## Arguments

- mat_file:

  A file (or path to file) in .mat format, exported from Flydra

- file_id:

  (Optional) identifier for this file. If not supplied, this defaults to
  `basename(file_name)`.

- subject_name:

  Name that will be assigned to the subject

- frame_rate:

  The capture frame rate of the session

- ...:

  Additional arguments that may be passed from other pathviewr functions

## Value

A tibble with numerical data in columns. The first two columns will have
frame numbers and time (assumed to be in secs), respectively. Columns 3
through 5 will contain position data. Note that unlike the behavior of
[`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)
this function produces "tidy" data that have already been gathered into
key-value pairs based on subject.

## See also

[`read_motive_csv`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)
for importing Motive data

Other data import functions:
[`as_viewr()`](https://docs.ropensci.org/pathviewr/reference/as_viewr.md),
[`import_and_clean_batch()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_batch.md),
[`import_batch()`](https://docs.ropensci.org/pathviewr/reference/import_batch.md),
[`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)

## Author

Vikram B. Baliga

## Examples

``` r
library(pathviewr)

## Import the example Flydra data included in the package
flydra_data <-
  read_flydra_mat(system.file("extdata", "pathviewr_flydra_example_data.mat",
                             package = 'pathviewr'),
                  subject_name = "birdie_wooster")

## Names of variables in the resulting tibble
names(flydra_data)
#>  [1] "frame"           "time_sec"        "subject"         "position_length"
#>  [5] "position_width"  "position_height" "velocity"        "length_inst_vel"
#>  [9] "width_inst_vel"  "height_inst_vel"

## A variety of metadata are stored as attributes. Of particular interest:
attr(flydra_data, "pathviewr_steps")
#> [1] "viewr"           "renamed_tunnel"  "gathered_tunnel"
```
