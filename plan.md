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
Problem,Description
"""Zombie"" VMs",Users leaving Virtual Machines active while not using them (High Idle Usage).,
Overprovisioning,Users selecting the largest machine size regardless of actual need.,
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


# Useful information
# Slide 1
Hello, my name is Ashraf and I am also a 3rd year software engineering apprentice like George.
I've been working with the Ada team to add carbon monitoring to their service. 
For those of you who don't know, Ada is a service that was formerly known as DAaaS.
Ada allows you to initiate and use virtual machines that are hosted
at the R86 data centre at RAL.

The purpose of this project is to provide the users of Ada with information that may lead them towards making greener choices in the future. 
We want users to know what impact they're having on the environment and what they can do reduce their impact.

# Slide 2
To achieve this, there are three main variables that we need to make the user aware of.
These are:
* Carbon intensity
* Electricity Usage
* Carbon Footprint

If users are aware of how their actions affect these three variables, they will be armed with the information necessary
to make the greenes choicest possible. They will be able to minimise their carbon footprint

# Slide 3
The first key variable is carbon intensity. As my colleague George has already explained, we 
can use the Carbon Intensity API to obtain a forecast of carbon intensity over the next 48 hours.

I've connected the API to a graph that will alow users to plan their usage of the service so that
they can minimise their carbon footprint. The graph, by default, shows the variation of carbon intensity over 
the current working day.
It highlights in green the 3 hour window where carbon intensity is at its lowest. 

If a user was to consult this graph and decide to use the service between 1 PM and 2 PM instead of between 9 AM and 10 AM,
their carbon emissions for that computation would be reduced by around 30 percent.
This is called time shifting and it is one of the most effective ways to reduce your carbon footprint. The value of the science 
that this hypothetical user produces would not be lessened by this small change but their impact on the planet would greatly be reduced.

This is a feature that has been proposed to the Ada team and will hopefully be on the platform soon. 

# Slide 4
The second key variable is electricity usage. It is important for a user to know how much electricity they are using to do their work
so that they can quantify the difference in the choices they make and hopefully see a difference over time as they make greener choices.

Now, unfortunately, Ada does not have accurate power metrics for its service. To get this information, I need to estimate.
The standard way of estimating electricity usage across various different applications such as Green Algorithms and CATS is 
to find out how long the CPU runs for and assign an assumed wattage for its usage. 

We seperate usage into busy and idle We assign 12 W as the cost of running a busy cpu and
we assign 1 W as the cost of running an idle cpu. 

We obtain data on CPU usage from Ada's prometheus database, which is a commonly used timeseries database for data centres.

We multiply the duration that a cpu has been active with the assumed wattage in order to get an estimate on that cpu's electricity usage.

# Slide 5
Using this information, we can determine the usage over time of an entire project. Here you can see the estimated electricity usage
of ISIS on the ada platform during the month of may. This is a graph that will hopefully become available on the ada platform
and is adjustable by Day, Month and Year. 

Idle usage is reprented by blue bars. Busy usage is represented by pink bars.
Idle usage is essentially wasted usage. It's usage that didn't contribute to any output. 
We're not trying to get users to stop using the platform entirely. They do have important work to do.
We're trying to get them to be efficient.
As you can see, this is currently not what is happening.

What are potential causes of this consistent and unnecessarily large idle usage?
There are two main contributors.

First is that many users leave their virtual machines active while they are not using them. Turning off 
a virtual machine isn't difficult. It's just pressing a button. But it doesn't happen automatically.

The second cause is overprovision.
In the Ada service, you are given a choice of machine size when you create a workspace.
You can make a workspace that has a few or many cpu cores assigned to it. 
Most users always pick the largest option. Often times this option is overkill for their needs.
Thus they are overprovisioned. 

Because users lack awareness of the cost of these decisions, they end up making unsustainable choices.
The solution is to give the users the information that they need. Most users, if they knew the cost of running a workspace idly,
would simply remember to turn off their workspaces. Many would consider picking the smaller machine size if they knew how much the 
larger options cost the planet. 


# Slide 6
The third key variable is Carbon Footprint. It's important to know how much this electricity usage contributes to carbon emissions.

In order to calculate this, we take the electricity usage that we just estimated in kwh.
We take the carbon intensity from the Carbon Intensity API, which is in gCo2eq/kwh.
We multiply these two variables together to get carbon footprint in gCo2eq.

# Slide 7
This allows us to create a similar graph to the previous one. Again, we have proposed these graphs to the Ada team and hope
that they will be implemented soon.

This time, we're looking as Carbon Footprint for the month of May. This time Idle usage is represented in green and 
busy usage is represented in orange.

# Slide 8
One thing you may note is that, while electricity usage is fairly consistent day to day, carbon usage varies dramatically across a given month.
This is because carbon intensity can vary dramatically on a day to day basis.

# Slide 9
Here is a sample to illustrate the point. On March 21st, we estimate that ISIS used approximately 92 Kwhs of electricity. This resulted 
in around 6.5 kgs of Co2eq emitted.

The very next day, ISIS used approximately 93 kwhs of electricity. This resulted in around 11 kgs of Co2 eq emitted into the atmosphere.

The usage didn't vary much across the two days. What changed dramatically was the average carbon intensity.
69 on March 21st and 124 on the 22nd.

This shows that changing the day that you do your computation can reduce your carbon footprint.

# Slide 10
In order to help users figure out which day is best easily, they can consult to the Carbon Intensity Forecast. 
This will allow them to see whether tomorrow or the day after will have a lower carbon intensity. 
Sometimes having an excuse to procrastinate can also help save the planet. 

# Slide 11
Now that we have data for the user's carbon footprint, it would be useful to show the totality of their usage
in a way that shows how green the decisions being made are.

I developed this graph to display this more intuitively than a bar chart. This is another feature that will be proposed to the Ada team
and hopefully implemented
This graph may look familiar to many of you. It is inspired by the Github commit history graph.
Instead of displaying commits over the course of a year, it displays carbon footprint.

Instead of varying from black to bright green, black being 0 commits in a day and bright green being many commits in a day,
it varies from green to red, with orange as an in between state. 
Green represents low carbon footprint. Red represents high carbon footprint. 

What you're seeing right now is the carbon footprint of ISIS over the last year. You may notice that there is a lot of missing data.
Unfortunately, the Prometheus database has significant gaps. 

The image that we see isn't pretty. It is, unfortunately, not as green as we'd like.

# Slide 12
If we recall back to the Carbon Usage graph, we can remind ourselves that most of this usage is idle and thus wasted.
This is good news. It means that adding carbon monitoring to the service could have a real impact.

I'd like to envision an alternate reality where ISIS users made greener choices. Where they turned off their idle machines
and picked machines that were suitable to their workload. 

To help your imagination, I've taken liberty of creating the same graph, with the same busy usage, but a more reasonable idle usage.

# Slide 13
This is what this alternate reality looks like. It's a lot greener. 

But how do we get there. What information could push the users to turn off their workspaces and choose smaller machines?

I have a couple of suggestions for the Ada team

# Slide 14

Here's a mock version of a workspace card in the Ada platform. It differs from the real version in that it tallies the 
current electricity and carbon usage of the workspace. It also seperates busy usage and idle usage. 
This would make the user aware of the carbon that they are wasting by leaving their workspace on for no reason.

Another suggestion is the implementation of carbon usage values for each machine size.
If users could see the cost of choosing the larger machine size, they may reconsider whether it is truly necessary.

These two changes may seem small but I'm a big believer in the idea that the only thing getting in the way of people making 
sustainable choices is a lack of awareness. STFC is an organisation filled with people who care about the environment. 
If you give them the information needed to make the right choice, they'll make the right choice.

Thank you for listening.
Now, my fellow apprentice George will tell you about his project. 