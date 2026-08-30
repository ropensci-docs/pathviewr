# Batch import of files for either Motive or Flydra (but not a mix of both)

Batch import of files for either Motive or Flydra (but not a mix of
both)

## Usage

``` r
import_batch(
  file_path_list,
  import_method = c("flydra", "motive"),
  file_id = NA,
  subject_name = NULL,
  frame_rate = NULL,
  simplify_marker_naming = TRUE,
  import_messaging = FALSE,
  ...
)
```

## Arguments

- file_path_list:

  A list of file paths

- import_method:

  Either "flydra" or "motive"

- file_id:

  Optional

- subject_name:

  For Flydra, the assigned subject name

- frame_rate:

  For Flydra, the assigned frame rate

- simplify_marker_naming:

  default TRUE; for Motive, whether marker naming should be simplified

- import_messaging:

  default FALSE; should this function report each time a file has been
  imported?

- ...:

  Additional arguments (may remove this if needed)

## Value

A list of viewr objects (tibble or data.frame with attribute
`pathviewr_steps` that includes `"viewr"`).

## Details

Refer to
[`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)
and
[`read_flydra_mat()`](https://docs.ropensci.org/pathviewr/reference/read_flydra_mat.md)
for details of data import methods.

## See also

Other data import functions:
[`as_viewr()`](https://docs.ropensci.org/pathviewr/reference/as_viewr.md),
[`import_and_clean_batch()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_batch.md),
[`read_flydra_mat()`](https://docs.ropensci.org/pathviewr/reference/read_flydra_mat.md),
[`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)

Other batch functions:
[`bind_viewr_objects()`](https://docs.ropensci.org/pathviewr/reference/bind_viewr_objects.md),
[`clean_viewr_batch()`](https://docs.ropensci.org/pathviewr/reference/clean_viewr_batch.md),
[`import_and_clean_batch()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_batch.md)

## Author

Vikram B. Baliga

## Examples

``` r
## Since we only have one example file of each type provided
## in pathviewr, we will simply import the same example multiple
## times to simulate batch importing. Replace the contents of
## the following list with your own list of files to be imported.

## Make a list of the same example file 3x
import_list <-
  c(rep(
    system.file("extdata", "pathviewr_motive_example_data.csv",
                package = 'pathviewr'),
    3
  ))

## Batch import
motive_batch_imports <-
  import_batch(import_list,
               import_method = "motive",
               import_messaging = TRUE)
#> File 1 imported.
#> File 2 imported.
#> File 3 imported.

## Batch cleaning of these imported files
## via clean_viewr_batch()
motive_batch_cleaned <-
  clean_viewr_batch(
    file_announce = TRUE,
    motive_batch_imports,
    desired_percent = 50,
    max_frame_gap = "autodetect",
    span = 0.95
  )
#> autodetect is an experimental feature -- please report issues.
#> File 1 has been cleaned successfully.
#> autodetect is an experimental feature -- please report issues.
#> File 2 has been cleaned successfully.
#> autodetect is an experimental feature -- please report issues.
#> File 3 has been cleaned successfully.

## Alternatively, use import_and_clean_batch() to
## combine import with cleaning on a batch of files
motive_batch_import_and_clean <-
  import_and_clean_batch(
    import_list,
    import_method = "motive",
    import_messaging = TRUE,
    motive_batch_imports,
    desired_percent = 50,
    max_frame_gap = "autodetect",
    span = 0.95
  )
#> File 1 imported.
#> File 2 imported.
#> File 3 imported.
#> autodetect is an experimental feature -- please report issues.
#> autodetect is an experimental feature -- please report issues.
#> autodetect is an experimental feature -- please report issues.

## Each of these lists of objects can be bound into
## one viewr object (i.e. one tibble) via
## bind_viewr_objects()
motive_bound_one <-
  bind_viewr_objects(motive_batch_cleaned)

motive_bound_two <-
  bind_viewr_objects(motive_batch_import_and_clean)

## Either route results in the same object ultimately:
identical(motive_bound_one, motive_bound_two)
#> [1] TRUE
```
