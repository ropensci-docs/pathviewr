# Plot trajectories and density plots of position by subject

Plots all trajectories and generates density plots of position by
subject from elevation and bird's eye views.

## Usage

``` r
plot_by_subject(obj_name, col_by_treat = FALSE, ...)
```

## Arguments

- obj_name:

  A viewr object (a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`) that has been passed
  through
  [`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md)
  or
  [`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md).

- col_by_treat:

  If multiple treatments or sessions, color data per treatment or
  session. Treatments must be levels in a column named `treatment`.

- ...:

  Additional arguments passed to/from other pathviewr functions.

## Value

A "bird's eye view" plot and an "elevation view" plot, made via ggplot2.

## Details

The input viewr object should have passed through
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md)
or
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md).
Optionally, treatments should have been added as levels in a column
named `treatment`. Two plots will be produced, one from a "bird's eye
view" of width against length and one from an "elevation view" of height
against length. All trajectories will be plotted on a per subject basis,
along with density plots of width or height depending on the view.
`col_by_treat = TRUE`, data will be plotted by color according to
treatment in both the trajectory plots and the density plots.

## See also

Other plotting functions:
[`plot_viewr_trajectories()`](https://docs.ropensci.org/pathviewr/reference/plot_viewr_trajectories.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

## Author

Melissa S. Armstrong

## Examples

``` r
library(pathviewr)
library(ggplot2)
library(magrittr)

if (interactive()) {
  ## Import the example Motive data included in the package
  motive_data <-
    read_motive_csv(system.file("extdata",
                                "pathviewr_motive_example_data.csv",
                                package = 'pathviewr'))

  ## Clean, isolate, and label trajectories
  motive_full <-
    motive_data %>%
    clean_viewr(desired_percent = 50,
                max_frame_gap = "autodetect",
                span = 0.95)

  ## Plot all trajectories by subject
  motive_full %>%
    plot_by_subject()

  ## Add treatment information
  motive_full$treatment <- c(rep("latA", 100), rep("latB", 100),
                             rep("latA", 100), rep("latB", 149))

  ## Plot all trajectories by subject, color by treatment
  motive_full %>%
    plot_by_subject(col_by_treat = TRUE)
}
```
