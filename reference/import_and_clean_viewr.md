# Import + clean_viewr()

Import a file and then, akin to `clean_viewr`, run through as many
cleaning steps as desired.

## Usage

``` r
import_and_clean_viewr(
  file_name,
  file_id = NA,
  relabel_viewr_axes = TRUE,
  gather_tunnel_data = TRUE,
  trim_tunnel_outliers = TRUE,
  standardization_option = "rotate_tunnel",
  get_velocity = TRUE,
  select_x_percent = TRUE,
  rename_viewr_characters = FALSE,
  separate_trajectories = TRUE,
  get_full_trajectories = TRUE,
  fill_traj_gaps = FALSE,
  ...
)
```

## Arguments

- file_name:

  Target file

- file_id:

  Optional

- relabel_viewr_axes:

  default TRUE, should axes be relabeled?

- gather_tunnel_data:

  default TRUE, should tunnel data be gathered?

- trim_tunnel_outliers:

  default TRUE, outliers be trimmed?

- standardization_option:

  default "rotate_tunnel"; which standardization option should be used?
  See Details for more.

- get_velocity:

  default TRUE, should velocity be computed?

- select_x_percent:

  default TRUE, should a region of interest be selected?

- rename_viewr_characters:

  default FALSE, should subjects be renamed?

- separate_trajectories:

  default TRUE, should trajectories be defined?

- get_full_trajectories:

  default TRUE, should only full trajectories be retained?

- fill_traj_gaps:

  default FALSE, should gaps in trajectories be filled?

- ...:

  Additional arguments passed to the corresponding functions.

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) that has passed through several `pathviewr`
functions as desired by the user, resulting in data that have been
cleaned and ready for analyses.

## Details

Each argument corresponds to a standalone function in `pathviewr`. E.g.
the parameter `relabel_viewr_axes` allows a user to choose whether
[`pathviewr::relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md)
is run internally. Should the user desire to use any non-default
parameter values for any functions included here, they should be
supplied to this function as additional arguments formatted exactly as
they would appear in their corresponding function(s). E.g. if the
"autodetect" feature in
[`pathviewr::separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md)
is desired, add an argument `max_frame_gap = "autodetect"` to the
arguments supplied to this function.

## See also

Other all in one functions:
[`clean_viewr()`](https://docs.ropensci.org/pathviewr/reference/clean_viewr.md)

## Author

Vikram B. Baliga

## Examples

``` r
library(pathviewr)

## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

motive_full <-
  motive_data %>%
  clean_viewr(desired_percent = 50,
              max_frame_gap = "autodetect",
              span = 0.95)
#> autodetect is an experimental feature -- please report issues.

## Alternatively, used the import_and_clean_viewr()
## function to combine these steps
motive_import_and_clean <-
  import_and_clean_viewr(
    file_name = system.file("extdata", "pathviewr_motive_example_data.csv",
                            package = 'pathviewr'),
    desired_percent = 50,
    max_frame_gap = "autodetect",
    span = 0.95
  )
#> autodetect is an experimental feature -- please report issues.
```
