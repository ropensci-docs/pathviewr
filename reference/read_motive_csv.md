# Import data from a CSV exported from Optitrack's Motive software

`read_motive_csv()` is designed to import data from a CSV that has been
exported from Optitrack's Motive software. The resultant object is a
tibble that additionally has important metadata stored as attributes
(see Details).

## Usage

``` r
read_motive_csv(file_name, file_id = NA, simplify_marker_naming = TRUE, ...)
```

## Arguments

- file_name:

  A file (or path to file) in CSV format

- file_id:

  (Optional) identifier for this file. If not supplied, this defaults to
  `basename(file_name)`.

- simplify_marker_naming:

  If Markers are encountered, should they be renamed from
  "Subject:marker" to "marker"? Defaults to TRUE

- ...:

  Additional arguments passed from other `pathviewr` functions

## Value

A tibble with numerical data in columns. The first two columns will have
frame numbers and time (assumed to be in secs), respectively. Columns 3
and beyond will contain the numerical data on the position or rotation
of rigid bodies and/or markers that appear in the Motive CSV file. Each
row corresponds to the position or rotation of all objects at a given
time (frame).

## Details

Uses
[`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html)
to import data from a CSV file and ultimately store it in a tibble. This
object is also labeled with the attribute `pathviewr_steps` with value
`viewr` to indicate that it has been imported by `pathviewr` and should
be friendly towards use with other functions in our package.
Additionally, the following metadata are stored in the tibble's
attributes: header information from the Motive CSV file (`header`),
original IDs for each object (`Motive_IDs`), the name of each subject in
each data column (`subject_names_full`) and unique values of subject
names (`subject_names_simple`), the type of data (rigid body or marker)
that appears in each column (`data_types_full`) and overall
(`data_types_simple`), and original data column names in the CSV
(`d1, d2`). See Example below for example code to inspect attributes.

## Warning

This function was written to read CSVs exported using Motive's Format
Version 1.23 and is not guaranteed to work with those from other
versions. Please file an Issue on our Github page if you encounter any
problems.

## See also

[`read_flydra_mat`](https://docs.ropensci.org/pathviewr/reference/read_flydra_mat.md)
for importing Flydra data

Other data import functions:
[`as_viewr()`](https://docs.ropensci.org/pathviewr/reference/as_viewr.md),
[`import_and_clean_batch()`](https://docs.ropensci.org/pathviewr/reference/import_and_clean_batch.md),
[`import_batch()`](https://docs.ropensci.org/pathviewr/reference/import_batch.md),
[`read_flydra_mat()`](https://docs.ropensci.org/pathviewr/reference/read_flydra_mat.md)

## Author

Vikram B. Baliga

## Examples

``` r
library(pathviewr)

## Import the example Motive data included in the package
motive_data <-
  read_motive_csv(system.file("extdata", "pathviewr_motive_example_data.csv",
                             package = 'pathviewr'))

## Names of variables in the resulting tibble
names(motive_data)
#>  [1] "frame"                      "time_sec"                  
#>  [3] "device02_rotation_x"        "device02_rotation_y"       
#>  [5] "device02_rotation_z"        "device02_rotation_w"       
#>  [7] "device02_position_x"        "device02_position_y"       
#>  [9] "device02_position_z"        "device02_mean_marker_error"
#> [11] "device03_rotation_x"        "device03_rotation_y"       
#> [13] "device03_rotation_z"        "device03_rotation_w"       
#> [15] "device03_position_x"        "device03_position_y"       
#> [17] "device03_position_z"        "device03_mean_marker_error"
#> [19] "device05_rotation_x"        "device05_rotation_y"       
#> [21] "device05_rotation_z"        "device05_rotation_w"       
#> [23] "device05_position_x"        "device05_position_y"       
#> [25] "device05_position_z"        "device05_mean_marker_error"

## A variety of metadata are stored as attributes. Of particular interest:
attr(motive_data, "pathviewr_steps")
#> [1] "viewr"
attr(motive_data, "file_id")
#> [1] "pathviewr_motive_example_data.csv"
attr(motive_data, "header")
#>                 metadata                      value
#> 1         Format Version                       1.23
#> 2              Take Name  sept-18_mixed-group_16-30
#> 3             Take Notes                           
#> 4     Capture Frame Rate                 100.000000
#> 5      Export Frame Rate                 100.000000
#> 6     Capture Start Time 2019-09-18 04.30.02.695 PM
#> 7   Total Frames in Take                     190951
#> 8  Total Exported Frames                     190951
#> 9          Rotation Type                 Quaternion
#> 10          Length Units                     Meters
#> 11      Coordinate Space                     Global
attr(motive_data, "Motive_IDs")
#>  [1] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [2] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [3] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [4] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [5] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [6] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [7] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [8] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [9] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [10] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [11] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [12] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [13] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [14] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [15] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [16] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [17] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [18] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [19] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [20] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [21] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [22] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [23] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [24] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
attr(motive_data, "subject_names_full")
#>  [1] "device02" "device02" "device02" "device02" "device02" "device02"
#>  [7] "device02" "device02" "device03" "device03" "device03" "device03"
#> [13] "device03" "device03" "device03" "device03" "device05" "device05"
#> [19] "device05" "device05" "device05" "device05" "device05" "device05"
attr(motive_data, "subject_names_simple")
#> [1] "device02" "device03" "device05"
attr(motive_data, "motive_data_names")
#> NULL
attr(motive_data, "motive_data_types_full")
#> NULL
attr(motive_data, "motive_data_types_simple")
#> NULL

## Of course, all attributes can be viewed as a (long) list via:
attributes(motive_data)
#> $names
#>  [1] "frame"                      "time_sec"                  
#>  [3] "device02_rotation_x"        "device02_rotation_y"       
#>  [5] "device02_rotation_z"        "device02_rotation_w"       
#>  [7] "device02_position_x"        "device02_position_y"       
#>  [9] "device02_position_z"        "device02_mean_marker_error"
#> [11] "device03_rotation_x"        "device03_rotation_y"       
#> [13] "device03_rotation_z"        "device03_rotation_w"       
#> [15] "device03_position_x"        "device03_position_y"       
#> [17] "device03_position_z"        "device03_mean_marker_error"
#> [19] "device05_rotation_x"        "device05_rotation_y"       
#> [21] "device05_rotation_z"        "device05_rotation_w"       
#> [23] "device05_position_x"        "device05_position_y"       
#> [25] "device05_position_z"        "device05_mean_marker_error"
#> 
#> $row.names
#>   [1]   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18
#>  [19]  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36
#>  [37]  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54
#>  [55]  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71  72
#>  [73]  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90
#>  [91]  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107 108
#> [109] 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126
#> [127] 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144
#> [145] 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162
#> [163] 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180
#> [181] 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198
#> [199] 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216
#> [217] 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234
#> [235] 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252
#> [253] 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270
#> [271] 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288
#> [289] 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305 306
#> [307] 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324
#> [325] 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342
#> [343] 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360
#> [361] 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378
#> [379] 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396
#> [397] 397 398 399 400 401 402 403 404 405 406 407 408 409 410 411 412 413 414
#> [415] 415 416 417 418 419 420 421 422 423 424 425 426 427 428 429 430 431 432
#> [433] 433 434 435 436 437 438 439 440 441 442 443 444 445 446 447 448 449 450
#> [451] 451 452 453 454 455 456 457 458 459 460 461 462 463 464 465 466 467 468
#> [469] 469 470 471 472 473 474 475 476 477 478 479 480 481 482 483 484 485 486
#> [487] 487 488 489 490 491 492 493 494 495 496 497 498 499 500 501 502 503 504
#> [505] 505 506 507 508 509 510 511 512 513 514 515 516 517 518 519 520 521 522
#> [523] 523 524 525 526 527 528 529 530 531 532 533 534 535 536 537 538 539 540
#> [541] 541 542 543 544 545 546 547 548 549 550 551 552 553 554 555 556 557 558
#> [559] 559 560 561 562 563 564 565 566 567 568 569 570 571 572 573 574 575 576
#> [577] 577 578 579 580 581 582 583 584 585 586 587 588 589 590 591 592 593 594
#> [595] 595 596 597 598 599 600 601 602 603 604 605 606 607 608 609 610 611 612
#> [613] 613 614 615 616 617 618 619 620 621 622 623 624 625 626 627 628 629 630
#> [631] 631 632 633 634 635 636 637 638 639 640 641 642 643 644 645 646 647 648
#> [649] 649 650 651 652 653 654 655 656 657 658 659 660 661 662 663 664 665 666
#> [667] 667 668 669 670 671 672 673 674 675 676 677 678 679 680 681 682 683 684
#> [685] 685 686 687 688 689 690 691 692 693 694 695 696 697 698 699 700 701 702
#> [703] 703 704 705 706 707 708 709 710 711 712 713 714 715 716 717 718 719 720
#> [721] 721 722 723 724 725 726 727 728 729 730 731 732 733 734 735 736 737 738
#> [739] 739 740 741 742 743 744 745 746 747 748 749 750 751 752 753 754 755 756
#> [757] 757 758 759 760 761 762 763 764 765 766 767 768 769 770 771 772 773 774
#> [775] 775 776 777 778 779 780 781 782 783 784 785 786 787 788 789 790 791 792
#> [793] 793 794 795 796 797 798 799 800 801 802 803 804 805 806 807 808 809 810
#> [811] 811 812 813 814 815 816 817 818 819 820 821 822 823 824 825 826 827 828
#> [829] 829 830 831 832 833 834 835 836 837 838 839 840 841 842 843 844 845 846
#> [847] 847 848 849 850 851 852 853 854 855 856 857 858 859 860 861 862 863 864
#> [865] 865 866 867 868 869 870 871 872 873 874 875 876 877 878 879 880 881 882
#> [883] 883 884 885 886 887 888 889 890 891 892 893 894 895 896 897 898 899 900
#> [901] 901 902 903 904 905 906 907 908 909 910 911 912 913 914 915 916 917 918
#> [919] 919 920 921 922 923 924 925 926 927 928 929 930 931 932 933 934
#> 
#> $class
#> [1] "tbl_df"     "tbl"        "data.frame"
#> 
#> $pathviewr_steps
#> [1] "viewr"
#> 
#> $file_id
#> [1] "pathviewr_motive_example_data.csv"
#> 
#> $file_mtime
#> [1] "2026-08-30 07:38:49 UTC"
#> 
#> $frame_rate
#> [1] 100
#> 
#> $header
#>                 metadata                      value
#> 1         Format Version                       1.23
#> 2              Take Name  sept-18_mixed-group_16-30
#> 3             Take Notes                           
#> 4     Capture Frame Rate                 100.000000
#> 5      Export Frame Rate                 100.000000
#> 6     Capture Start Time 2019-09-18 04.30.02.695 PM
#> 7   Total Frames in Take                     190951
#> 8  Total Exported Frames                     190951
#> 9          Rotation Type                 Quaternion
#> 10          Length Units                     Meters
#> 11      Coordinate Space                     Global
#> 
#> $Motive_IDs
#>  [1] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [2] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [3] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [4] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [5] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [6] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [7] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [8] "\"9E207518D8A311E969D7AB6B1FACE49B\""
#>  [9] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [10] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [11] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [12] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [13] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [14] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [15] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [16] "\"B88E118D8A411E969D7AB6B1FACE49B\"" 
#> [17] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [18] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [19] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [20] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [21] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [22] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [23] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> [24] "\"CDF1C735D8A411E969D7AB6B1FACE49B\""
#> 
#> $subject_names_full
#>  [1] "device02" "device02" "device02" "device02" "device02" "device02"
#>  [7] "device02" "device02" "device03" "device03" "device03" "device03"
#> [13] "device03" "device03" "device03" "device03" "device05" "device05"
#> [19] "device05" "device05" "device05" "device05" "device05" "device05"
#> 
#> $subject_names_simple
#> [1] "device02" "device03" "device05"
#> 
#> $data_names
#>  [1] "frame"                      "time_sec"                  
#>  [3] "device02_rotation_x"        "device02_rotation_y"       
#>  [5] "device02_rotation_z"        "device02_rotation_w"       
#>  [7] "device02_position_x"        "device02_position_y"       
#>  [9] "device02_position_z"        "device02_mean_marker_error"
#> [11] "device03_rotation_x"        "device03_rotation_y"       
#> [13] "device03_rotation_z"        "device03_rotation_w"       
#> [15] "device03_position_x"        "device03_position_y"       
#> [17] "device03_position_z"        "device03_mean_marker_error"
#> [19] "device05_rotation_x"        "device05_rotation_y"       
#> [21] "device05_rotation_z"        "device05_rotation_w"       
#> [23] "device05_position_x"        "device05_position_y"       
#> [25] "device05_position_z"        "device05_mean_marker_error"
#> 
#> $data_types_full
#>  [1] "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body"
#>  [6] "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body"
#> [11] "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body"
#> [16] "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body"
#> [21] "Rigid Body" "Rigid Body" "Rigid Body" "Rigid Body"
#> 
#> $data_types_simple
#> [1] "Rigid Body"
#> 
#> $d1
#>  [1] ""                  ""                  "Rotation"         
#>  [4] "Rotation"          "Rotation"          "Rotation"         
#>  [7] "Position"          "Position"          "Position"         
#> [10] "Mean Marker Error" "Rotation"          "Rotation"         
#> [13] "Rotation"          "Rotation"          "Position"         
#> [16] "Position"          "Position"          "Mean Marker Error"
#> [19] "Rotation"          "Rotation"          "Rotation"         
#> [22] "Rotation"          "Position"          "Position"         
#> [25] "Position"          "Mean Marker Error"
#> 
#> $d2
#>  [1] "Frame"          "Time (Seconds)" "X"              "Y"             
#>  [5] "Z"              "W"              "X"              "Y"             
#>  [9] "Z"              ""               "X"              "Y"             
#> [13] "Z"              "W"              "X"              "Y"             
#> [17] "Z"              ""               "X"              "Y"             
#> [21] "Z"              "W"              "X"              "Y"             
#> [25] "Z"              ""              
#> 
#> $import_method
#> [1] "motive"
#> 
```
