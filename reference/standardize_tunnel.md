# Rotate and center a tunnel based on landmarks

Similar to
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md);
rotate and center tunnel data based on landmarks (specific subjects in
the data).

## Usage

``` r
standardize_tunnel(
  obj_name,
  landmark_one = "perch1",
  landmark_two = "perch2",
  ...
)
```

## Arguments

- obj_name:

  The input viewr object; a tibble or data.frame with attribute
  `pathviewr_steps` that includes `"viewr"` that has been passed through
  [`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md)
  and
  [`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md)
  (or is structured as though it has been passed through those
  functions).

- landmark_one:

  Subject name of the first landmark

- landmark_two:

  Subject name of the second landmark

- ...:

  Additional arguments passed to/from other pathviewr functions

## Value

A viewr object (tibble or data.frame with attribute `pathviewr_steps`
that includes `"viewr"`) in which data have been rotated according to
the positions of the landmarks in the data.

## Details

The center point of the tunnel is estimated as the point between the two
landmarks. It is therefore recommended that `landmark_one` and
`landmark_two` be objects that are placed on opposite ends of the tunnel
(e.g. in an avian flight tunnel, these landmarks may be perches that are
placed at the extreme ends). The angle between landmark_one,
tunnel_center_point, and arbitrary point along the length axis
(tunnel_center_point - 1 on length) is estimated. That angle is then
used to rotate the data, again only in the length and width dimensions.
Height is standardized by average landmark height; values greater than 0
are above the landmarks and values less than 0 are below the landmark
level.

## Warning

The `position_length` values of landmark_one MUST be less than the
`position_length` values of landmark_two; otherwise, the rotation will
apply to a mirror-image of the tunnel

## See also

Other data cleaning functions:
[`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md),
[`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md),
[`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md),
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md),
[`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md),
[`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md),
[`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md),
[`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md),
[`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)

Other tunnel standardization functions:
[`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md),
[`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md)

## Author

Vikram B. Baliga

## Examples

``` r
## Example data that would work with this function are
## not included in this version of pathviewr. Please
## contact the package authors for further guidance
## should you need it.
```
