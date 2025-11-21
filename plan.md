# Poster style
* Minimalist
* Understandable from a distance
* A0
* Portrait
* Written in Nuxt
* Colours and shapes used to direct eyes

# Poster Presenter
* Ashraf Hussain
* ashraf.hussain@stfc.ac.uk

# Poster Structure
STFC Logo - Title - Poster Presenter
Project Abstract
Carbon Footprint Equation
Electricity Segment
Carbon Intensity Segment
Carbon Footprint Segment


# Elements

## STFC Logo
* stfc_logo.png
## Title
* From Metrics to Mitigation: Visualizing and Reducing the Carbon Footprint of STFC’s Ada Cloud Computing Service

## Project Abstract
This project presents a suite of interactive visual tools designed to monitor, forecast, and reduce carbon intensity and energy usage. 
The Carbon Intensity Forecast visualizes predicted carbon intensity over a 48-hour period, enabling users to schedule activities during low-impact periods, 
with highlighted windows indicating the greenest operating times. 
Complementing this, Usage Graphs display electricity consumption and associated carbon emissions, broken down by project, machine, experiment, 
or user—revealing inefficiencies such as excessive idle usage in ISIS workspaces. 
A GitHub-style heatmap offers an intuitive, color-coded overview of daily carbon footprint trends, helping users quickly assess whether their operations are becoming greener over time. 
Additional features include workspace tracking, allowing individuals to monitor energy and carbon metrics in real time, and machine size usage tracking, providing average emission data to encourage efficient resource choices. 
Together, these tools aim to raise awareness, promote sustainability, and support data-driven decision-making within the STFC community. 

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
Problems
* ~60% of electricity usage is idle
* Why?
    * "Zombie" VMs": Users leaving Virtual Machines active while not using them.
    * Overprovisioning: Users selecting the largest machine size regardless of actual need.
### How can we use this data to reduce carbon footprint?
 
* Workspace tracker
    * workspace_tracker.png
    * Implementing a workspace tracking card that shows the user how much idle electricity usage and thus waste carbon emisions their workspace has used thus far. This is to encourage them 
    to turn off their workspaces.
* Upfront Costing: Display carbon usage values for each machine size before the user creates the workspace.


## Carbon Intensity Segment
* Red background

### How do we get this data?
* carbon_intensity_api_logo.png
```
 The Carbon Intensity API (from NESO/National Grid ESO) is an open, machine-learning–driven web service that provides real-time and 
forecast data on how carbon-intensive electricity is in Great Britain, expressed in grams of CO₂ per kWh. 
It exposes programmatic endpoints for both national and regional views, giving historic, current, and up-to-96-hours-ahead estimates based on the generation mix (renewables, nuclear, fossil fuels, imports, etc.), 
allowing apps, devices, and services
to schedule their electricity use at times when the grid is “cleaner” and thereby reduce associated emissions.
```

### What does this data show us?
* generation_mix.png
```
In the context of the Carbon Intensity API and the GB grid, the generation mix is simply the breakdown of how electricity is being produced at any given moment
—how much is coming from sources like wind, solar, nuclear, hydro, gas, coal, biomass, and interconnectors (imports from other countries). 
Each of those technologies has a different carbon footprint, so the mix directly determines the grid’s overall carbon intensity in grams of CO₂ per kWh. 
When there’s lots of wind and solar on the system, for example, the mix is “greener” and carbon intensity goes down; when gas and especially coal dominate, it goes up.
The API exposes this mix in its data so that developers and users can see not just how dirty or clean the grid is, 
but why—and then choose to shift usage to periods where low-carbon sources make up a bigger share.
```

### How can we use this data to reduce carbon footprint?
* carbon_intensity_forecast.png
```
The Carbon Intensity Forecast widget makes time-shifting really simple: it shows how “clean” or “dirty” the grid is expected to be throughout the day,
so you can move flexible electricity use into the greenest hours. The line chart plots the forecast carbon intensity in gCO₂/kWh,
and features like the shaded working-day window and the highlighted “Best 3h window” help you quickly spot when emissions will be lowest.
By scheduling things like EV charging, washing machines, dishwashers, or data-heavy computing tasks into those low-carbon periods—and avoiding the higher peaks at the edges of the day—
you keep your lifestyle the same but reduce the emissions associated with your electricity use.
```

## Carbon Footprint Segment
* Green background

### Potential Impact
```
The GitHub-style carbon footprint heatmap shows a whole year of activity at a glance by representing each day as a small square in a calendar grid, 
just like the familiar commit history view on GitHub. Instead of counting code commits, each square encodes the total carbon footprint from Ada workspace usage on that day. 
The colour ranges from green (low carbon footprint) through orange to red (high carbon footprint), so long stretches of red quickly reveal periods of heavy or wasteful usage,
while greener patches indicate days where users either ran fewer workloads, chose smaller machine sizes, made good use of time-shifting, or switched off idle workspaces.
Because it aggregates both busy and idle usage into a simple visual summary, the heatmap lets users intuitively see how their decisions over the year add up for the planet,
and highlights how much cleaner things could look if they reduced unnecessary idle time and avoided overprovisioning.
```

* Actual Github graph intro
    * actual_github_commit_history_style_carbon_footprint_heatmap.png

* Idealised Github graph intro
    * idealised_github_commit_history_style_carbon_footprint_heatmap.png


