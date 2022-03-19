GDAC Capstone
================

<!-- README.md is generated from README.Rmd. Please edit that file -->

**WORK IN PROGRESS**

This is the capstone project for the [Google Data Analytics
Certificate](https://www.coursera.org/professional-certificates/google-data-analytics?)
available through [Coursera](https://www.coursera.org/)

For my capstone, I chose to complete Track 1 with the *Cyclistic*
bike-share case study.

Background information about the case study can be found in the `info`
folder.

**Note About Code**: I tried to included the package name the first time
I use a function. Like this `rio::import`.

# **Question to Answer**

How do annual members and casual riders use Cyclistic bikes differently?

You will produce a report with the following deliverables:

1.  A clear statement of the business task
2.  A description of all data sources used
3.  Documentation of any cleaning or manipulation of data
4.  A summary of your analysis
5.  Supporting visualizations and key findings
6.  Your top three recommendations based on your analysis

# **Business Task**

The business task is to compare casual and member riders to help develop
a strategy to convert casual riders to member riders.

# **Data Source:**

This data is made available by [Divvy
Bikes](https://ride.divvybikes.com/data-license-agreement) for use, the
name of the company has just been changed. Data is available
[here](https://divvy-tripdata.s3.amazonaws.com/index.html).

``` r
# import 1 file to see structure
march_2021 <- rio::import(here::here("bike_data", "202103-divvy-tripdata.csv"), 
                          setclass = "tibble")

# create list of all file names
bike_files <- list.files(here("bike_data"), pattern = ".csv", full.names = TRUE)

# import all files and combine into one tibble
bikes_raw <- bike_files %>% 
  lapply(import, setclass = "tibble") %>% 
  dplyr::bind_rows()

rio::export(bikes, file = hehere("bike_data", "all_bikes.rds"))
```

# Data Wrangling

``` r
bikes <- bikes_raw %>% 
  mutate(ride_length = difftime(ended_at, started_at, units = "mins"))
```

``` r
bikes %>% 
  group_by(member_casual) %>% 
  summarize(number = n(), across(ride_length, c(mean = mean))) %>% 
  gt::gt()
```

<div id="evmqlahuee" style="overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#evmqlahuee .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#evmqlahuee .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#evmqlahuee .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#evmqlahuee .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 0;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#evmqlahuee .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#evmqlahuee .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#evmqlahuee .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#evmqlahuee .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#evmqlahuee .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#evmqlahuee .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#evmqlahuee .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#evmqlahuee .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
}

#evmqlahuee .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#evmqlahuee .gt_from_md > :first-child {
  margin-top: 0;
}

#evmqlahuee .gt_from_md > :last-child {
  margin-bottom: 0;
}

#evmqlahuee .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#evmqlahuee .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#evmqlahuee .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#evmqlahuee .gt_row_group_first td {
  border-top-width: 2px;
}

#evmqlahuee .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#evmqlahuee .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#evmqlahuee .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#evmqlahuee .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#evmqlahuee .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#evmqlahuee .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#evmqlahuee .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#evmqlahuee .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#evmqlahuee .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#evmqlahuee .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-left: 4px;
  padding-right: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#evmqlahuee .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#evmqlahuee .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#evmqlahuee .gt_left {
  text-align: left;
}

#evmqlahuee .gt_center {
  text-align: center;
}

#evmqlahuee .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#evmqlahuee .gt_font_normal {
  font-weight: normal;
}

#evmqlahuee .gt_font_bold {
  font-weight: bold;
}

#evmqlahuee .gt_font_italic {
  font-style: italic;
}

#evmqlahuee .gt_super {
  font-size: 65%;
}

#evmqlahuee .gt_footnote_marks {
  font-style: italic;
  font-weight: normal;
  font-size: 75%;
  vertical-align: 0.4em;
}

#evmqlahuee .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#evmqlahuee .gt_slash_mark {
  font-size: 0.7em;
  line-height: 0.7em;
  vertical-align: 0.15em;
}

#evmqlahuee .gt_fraction_numerator {
  font-size: 0.6em;
  line-height: 0.6em;
  vertical-align: 0.45em;
}

#evmqlahuee .gt_fraction_denominator {
  font-size: 0.6em;
  line-height: 0.6em;
  vertical-align: -0.05em;
}
</style>
<table class="gt_table">
  
  <thead class="gt_col_headings">
    <tr>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1">member_casual</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1">number</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1">ride_length_mean</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td class="gt_row gt_left">casual</td>
<td class="gt_row gt_right">2540693</td>
<td class="gt_row gt_center">31.92026985026</td></tr>
    <tr><td class="gt_row gt_left">member</td>
<td class="gt_row gt_right">3127293</td>
<td class="gt_row gt_center">13.4844657024462</td></tr>
  </tbody>
  
  
</table>
</div>
