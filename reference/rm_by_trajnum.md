# Remove subjects by trajectory number

Specify a minimum number of trajectories that each subject must complete
during a treatment, trial, or session.

## Usage

``` r
rm_by_trajnum(
  obj_name,
  trajnum = 5,
  mirrored = FALSE,
  treatment1,
  treatment2,
  ...
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"`. Trajectories must be
  predefined (i.e. via
  [`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md)).

- trajnum:

  Minimum number of trajectories; must be numeric.

- mirrored:

  Does the data have mirrored treatments? If so, arguments `treatment1`
  and `treatment2` must also be provided, indicating the names of two
  mirrored treatments, both of which must meet the trajectory threshold
  specified in `trajnum`. Default is FALSE.

- treatment1:

  The first treatment or session during which the threshold must be met.

- treatment2:

  A second treatment or session during which the threshold must be met.

- ...:

  Additional arguments passed to/from other pathviewr functions.

## Value

A viewr object; a tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"` that now has fewer observations (rows) as a
result of removal of subjects with too few trajectories according to the
`trajnum` parameter.

## Details

Depending on analysis needs, users may want to remove subjects that have
not completed a certain number of trajectories during a treatment,
trial, or session. If `mirrored = FALSE`, no treatment information is
necessary and subjects will be removed based on total number of
trajectories as specified in `trajnum`. If `mirrored = TRUE`, the
`treatment1` and `treatment2` parameters will allow users to define
during which treatments or sessions subjects must reach threshold as
specified in the `trajnum` argument. For example, if `mirrored = TRUE`,
setting `treatment1 = "latA"`, `treatment2 = "latB"` and `trajnum = 5`
will remove subjects that have fewer than 5 trajectories during the
`"latA"` treatment AND the `"latB"` treatment. `treatment1` and
`treatment2` should be levels within a column named `"treatment"`.

## Author

Melissa S. Armstrong

## Examples

``` r
library(pathviewr)

## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                              package = 'pathviewr'))

## Clean, isolate, and label trajectories
motive_full <-
  motive_data %>%
  clean_viewr(desired_percent = 50,
              max_frame_gap = "autodetect",
              span = 0.95)
#> autodetect is an experimental feature -- please report issues.

##Remove subjects that have not completed at least 150 trajectories:
motive_rm_unmirrored <-
  motive_full %>%
  rm_by_trajnum(trajnum = 150)
#> Joining with `by = join_by(subject)`

## Add treatment information
motive_full$treatment <- c(rep("latA", 100),
                           rep("latB", 100),
                           rep("latA", 100),
                           rep("latB", 149))

## Remove subjects by that have not completed at least 10 trajectories in
## both treatments
motive_rm_mirrored <-
  motive_full %>%
  rm_by_trajnum(
    trajnum = 10,
    mirrored = TRUE,
    treatment1 = "latA",
    treatment2 = "latB"
  )
#> Joining with `by = join_by(subject)`
```
