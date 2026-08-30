# Package index

## Data import functions

Functions for creating ‘viewr’ objects from external data

- [`read_motive_csv()`](https://docs.ropensci.org/pathviewr/reference/read_motive_csv.md)
  : Import data from a CSV exported from Optitrack's Motive software
- [`read_flydra_mat()`](https://docs.ropensci.org/pathviewr/reference/read_flydra_mat.md)
  : Import data from a MAT file exported from Flydra software
- [`as_viewr()`](https://docs.ropensci.org/pathviewr/reference/as_viewr.md)
  : Convert data from another format into a viewr object

## Utility functions

Functions for wrangling and cleaning ‘viewr’ objects

- [`get_header_viewr()`](https://docs.ropensci.org/pathviewr/reference/get_header_viewr.md)
  : Extract header info from imported viewr object

- [`relabel_viewr_axes()`](https://docs.ropensci.org/pathviewr/reference/relabel_viewr_axes.md)
  : Relabel the dimensions as length, width, and height

- [`gather_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/gather_tunnel_data.md)
  : Gather data columns into key-value pairs

- [`rescale_tunnel_data()`](https://docs.ropensci.org/pathviewr/reference/rescale_tunnel_data.md)
  :

  Rescale position data within a `viewr` object

- [`rename_viewr_characters()`](https://docs.ropensci.org/pathviewr/reference/rename_viewr_characters.md)
  : Rename subjects in the data via pattern detection

- [`trim_tunnel_outliers()`](https://docs.ropensci.org/pathviewr/reference/trim_tunnel_outliers.md)
  : Trim out artifacts and other outliers from the extremes of the
  tunnel

- [`rotate_tunnel()`](https://docs.ropensci.org/pathviewr/reference/rotate_tunnel.md)
  : Rotate a tunnel so that perches are approximately aligned

- [`standardize_tunnel()`](https://docs.ropensci.org/pathviewr/reference/standardize_tunnel.md)
  : Rotate and center a tunnel based on landmarks

- [`redefine_tunnel_center()`](https://docs.ropensci.org/pathviewr/reference/redefine_tunnel_center.md)
  : "Center" the tunnel data, i.e. translation but no rotation

- [`select_x_percent()`](https://docs.ropensci.org/pathviewr/reference/select_x_percent.md)
  : Select a region of interest within the tunnel

- [`quick_separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/quick_separate_trajectories.md)
  : Quick version of separate_trajectories()

- [`separate_trajectories()`](https://docs.ropensci.org/pathviewr/reference/separate_trajectories.md)
  : Separate rows of data into separately labeled trajectories.

- [`get_full_trajectories()`](https://docs.ropensci.org/pathviewr/reference/get_full_trajectories.md)
  : Retain trajectories that span a selected region of interest

- [`section_tunnel_by()`](https://docs.ropensci.org/pathviewr/reference/section_tunnel_by.md)
  : Bin data along a specified axis

- [`exclude_by_velocity()`](https://docs.ropensci.org/pathviewr/reference/exclude_by_velocity.md)
  : Remove trajectories entirely, based on velocity thresholds

- [`fill_traj_gaps()`](https://docs.ropensci.org/pathviewr/reference/fill_traj_gaps.md)
  : Interpolate gaps within trajectories

- [`rm_by_trajnum()`](https://docs.ropensci.org/pathviewr/reference/rm_by_trajnum.md)
  : Remove subjects by trajectory number

- [`insert_treatments()`](https://docs.ropensci.org/pathviewr/reference/insert_treatments.md)
  : Inserts treatment and experiment information

- [`set_traj_frametime()`](https://docs.ropensci.org/pathviewr/reference/set_traj_frametime.md)
  : Redefine frames and time stamps on a per-trajectory basis

- [`clean_by_span()`](https://docs.ropensci.org/pathviewr/reference/clean_by_span.md)
  : Remove file_sub_traj entries that do not span the full region of
  interest

- [`remove_duplicate_frames()`](https://docs.ropensci.org/pathviewr/reference/remove_duplicate_frames.md)
  : Remove any duplicates or aliased frames within trajectories

- [`remove_vel_anomalies()`](https://docs.ropensci.org/pathviewr/reference/remove_vel_anomalies.md)
  : Remove any rows which show sharp shifts in velocity that are likely
  due to tracking errors

## Analytical functions

Functions for quantitative analysis

- [`find_curve_elbow()`](https://docs.ropensci.org/pathviewr/reference/find_curve_elbow.md)
  : Find the "elbow" of a curve.
- [`get_velocity()`](https://docs.ropensci.org/pathviewr/reference/get_velocity.md)
  : Get instantaneous velocity for subjects
- [`get_traj_velocities()`](https://docs.ropensci.org/pathviewr/reference/get_traj_velocities.md)
  : Recompute trajectory-specific velocities
- [`calc_min_dist_box()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_box.md)
  : Calculate minimum distance to lateral and end walls in a box-shaped
  experimental tunnel
- [`calc_min_dist_v()`](https://docs.ropensci.org/pathviewr/reference/calc_min_dist_v.md)
  : Calculate minimum distance to lateral and end walls in a V-shaped
  experimental tunnel
- [`get_vis_angle()`](https://docs.ropensci.org/pathviewr/reference/get_vis_angle.md)
  : Estimate visual angles from a subject's perspective in an
  experimental tunnel
- [`get_sf()`](https://docs.ropensci.org/pathviewr/reference/get_sf.md)
  : Estimate the spatial frequency of visual stimuli from the subject's
  perspective in an experimental tunnel.
- [`get_dist_point_line()`](https://docs.ropensci.org/pathviewr/reference/get_dist_point_line.md)
  : Compute distance between a point and a line
- [`get_3d_cross_prod()`](https://docs.ropensci.org/pathviewr/reference/get_3d_cross_prod.md)
  : Compute the cross product of two 3D vectors
- [`rad_2_deg()`](https://docs.ropensci.org/pathviewr/reference/rad_2_deg.md)
  : Convert radians to degrees
- [`deg_2_rad()`](https://docs.ropensci.org/pathviewr/reference/deg_2_rad.md)
  : Convert degrees to radians
- [`get_2d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_2d_angle.md)
  : Compute an angle in 2D space
- [`get_3d_angle()`](https://docs.ropensci.org/pathviewr/reference/get_3d_angle.md)
  : Compute an angle in 3D space

## Plotting functions

Functions for plotting ‘viewr’ objects

- [`visualize_frame_gap_choice()`](https://docs.ropensci.org/pathviewr/reference/visualize_frame_gap_choice.md)
  : Visualize the consequence of using various max_frame_gap values
- [`plot_viewr_trajectories()`](https://docs.ropensci.org/pathviewr/reference/plot_viewr_trajectories.md)
  : Plot each trajectory within a viewr object
- [`plot_by_subject()`](https://docs.ropensci.org/pathviewr/reference/plot_by_subject.md)
  : Plot trajectories and density plots of position by subject

## All-in-one functions

Complete data import and cleaning pipelines

- [`clean_viewr()`](https://docs.ropensci.org/pathviewr/reference/clean_viewr.md)
  : All-in-one function to clean imported objects
- [`import_and_clean_viewr()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_viewr.md)
  : Import + clean_viewr()

## Batch analysis functions

Functions for the analysis of multiple files or `viewr` objects

- [`import_batch()`](https://docs.ropensci.org/pathviewr/reference/import_batch.md)
  : Batch import of files for either Motive or Flydra (but not a mix of
  both)
- [`clean_viewr_batch()`](https://docs.ropensci.org/pathviewr/reference/clean_viewr_batch.md)
  : Batch clean viewr files
- [`import_and_clean_batch()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_batch.md)
  : Batch import and clean files
- [`bind_viewr_objects()`](https://docs.ropensci.org/pathviewr/reference/bind_viewr_objects.md)
  : Bind viewr objects
