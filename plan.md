# Elements

## STFC Logo
* stfc_logo.png
## Title
* From Metrics to Mitigation: Visualizing and Reducing the Carbon Footprint of STFC’s Ada Cloud Computing Service

## Project Abstract

## Carbon Footprint Equation
* Electricity (kwh) * Carbon Intensity (gCO2eq/kwh) = Carbon Footprint (gCO2eq)

## Electricity Segment
* Blue background

### How do we get this data?
* prometheus_logo.png
* Pull node_cpu_seconds_total from Ada's Prometheus Database (Both idle and busy cpu usage)
* Assume that a cpu core uses 12 W when busy, 1 W when idle
* Estimate electricity usage

### What does this data show us?
* idle vs busy usage
    * estimated_usage_bar_chart.png

### How can we use this data to reduce carbon footprint?
* Workspace tracker
    * workspace_tracker.png
    * A common 
    * Implementing a workspace tracking card that shows the user how much idle electricity usage their 


## Carbon Intensity Segment
* Red background

### How do we get this data?
* carbon_intensity_api_logo.png
* Carbon Intensity API ramble

### What does this data show us?
* generation_mix.png
* generation mix ramble

### How can we use this data to reduce carbon footprint?
* carbon_intensity_forecast.png
* time shifting ramble

## Carbon Footprint Segment
* Green background

### Potential Impact
* Github commit history style carbon footprint heatmap explanation

* Actual Github graph intro
    * actual_github_commit_history_style_carbon_footprint_heatmap.png

* Ideadlised Github graph intro
    * idealised_github_commit_history_style_carbon_footprint_heatmap.png

* potential impact ramble