<template>
  <main class="poster">
   <header class="poster-header">
    <div class="logo">
      <img src="/images/stfc_logo.png" alt="STFC logo">
    </div>

    <div class="title-block">
      <h1>From Metrics to Mitigation: Visualizing and Reducing the Carbon Footprint of STFC’s Ada Cloud Computing Service</h1>
    </div>

    <div class="presenter">
      <p class="name">Ashraf Hussain</p>
      <p class="email">ashraf.hussain@stfc.ac.uk</p>
    </div>
  </header>


  <section class="abstract">
  <h2>Project Abstract</h2>
  <p>This project presents a suite of interactive visual tools designed to monitor, forecast, and reduce carbon intensity and energy usage. 
The Carbon Intensity Forecast visualizes predicted carbon intensity over a 48-hour period, enabling users to schedule activities during low-impact periods, 
with highlighted windows indicating the greenest operating times. 
Complementing this, Usage Graphs display electricity consumption and associated carbon emissions, broken down by project, machine, experiment, 
or user—revealing inefficiencies such as excessive idle usage in ISIS workspaces. 
A GitHub-style heatmap offers an intuitive, color-coded overview of daily carbon footprint trends, helping users quickly assess whether their operations are becoming greener over time. 
Additional features include workspace tracking, allowing individuals to monitor energy and carbon metrics in real time, and machine size usage tracking, providing average emission data to encourage efficient resource choices. 
Together, these tools aim to raise awareness, promote sustainability, and support data-driven decision-making within the STFC community. </p>
  </section>

  <section class="equation">
    <h2>Carbon Footprint Equation</h2>
    <p>Electricity (kWh) × Carbon Intensity (gCO₂eq/kWh) = Carbon Footprint (gCO₂eq)</p>
  </section>



  <article class="segment segment-electricity">
  <h2>Electricity</h2>

  <section>
    <h3>How do we get this data?</h3>
    <div class="inline-logo">
      <img src="/images/prometheus_logo.png" alt="Prometheus" />
    </div>
    <ul>
      <li>Pull <code>node_cpu_seconds_total</code> from Ada's Prometheus Database (Both idle and busy cpu usage)</li>
      <li>Assume that a cpu core uses 12 W when busy, 1 W when idle</li>
    </ul>
  </section>

  <section>
    <h3>What does this data show us?</h3>
    <img
      src="/images/estimated_usage_bar_chart.png"
      alt="Idle vs busy electricity usage chart"
      class="segment-image"
    />
    <ul>
      <li>~60% of electricity usage is idle</li>
      <li>Why?</li>
      <ul>
        <li>"Zombie" VMs: Users leaving Virtual Machines active while not using them.</li>
        <li>Overprovisioning: Users selecting the largest machine size regardless of actual need.</li>
      </ul>
    </ul>
  </section>

  <section>
    <h3>How can we use this to reduce carbon footprint?</h3>
    <p>Highlight wasteful idle usage and encourage users to shut down workspaces.</p>
    <img
      src="/images/workspace_tracker.png"
      alt="Workspace tracker UI"
      class="segment-image"
    />
<ul>
  <li>Workspace tracker
    <ul>
      <li>workspace_tracker.png</li>
      <li>Implementing a workspace tracking card that shows the user how much idle electricity usage and thus waste carbon emisions their workspace has used thus far. This is to encourage them 
    to turn off their workspaces.</li>
    </ul>
  </li>
  <li>Upfront Costing: Display average carbon usage values for each machine size before the user creates the workspace.</li>
</ul>


    </section>
  </article>

  <!-- Carbon Intensity Segment Content -->
  <article class="segment segment-intensity">
  <h2>Carbon Intensity</h2>

  <section>
    <h3>How do we get this data?</h3>
    <img
      src="/images/carbon_intensity_api_logo.png"
      alt="Carbon Intensity API"
      class="inline-logo-img"
    />
    <ul> The Carbon Intensity API (from NESO/National Grid ESO) is an open, machine-learning–driven web service that provides real-time and 
forecast data on how carbon-intensive electricity is in Great Britain, expressed in grams of CO₂ per kWh. 
It exposes programmatic endpoints for both national and regional views, giving historic, current, and up-to-96-hours-ahead estimates based on the generation mix (renewables, nuclear, fossil fuels, imports, etc.), 
allowing apps, devices, and services
to schedule their electricity use at times when the grid is “cleaner” and thereby reduce associated emissions.
</ul>
</section>

  <section>
    <h3>What does this data show us?</h3>
    <img
      src="/images/generation_mix.png"
      alt="Generation mix"
      class="segment-image"
    />
    <p>In the context of the Carbon Intensity API and the GB grid, the generation mix is simply the breakdown of how electricity is being produced at any given moment
—how much is coming from sources like wind, solar, nuclear, hydro, gas, coal, biomass, and interconnectors (imports from other countries). 
Each of those technologies has a different carbon footprint, so the mix directly determines the grid’s overall carbon intensity in grams of CO₂ per kWh. 
When there’s lots of wind and solar on the system, for example, the mix is “greener” and carbon intensity goes down; when gas and especially coal dominate, it goes up.
The API exposes this mix in its data so that developers and users can see not just how dirty or clean the grid is, 
but why—and then choose to shift usage to periods where low-carbon sources make up a bigger share.</p>
  </section>

  <section>
    <h3>How can we reduce footprint?</h3>
    <img
      src="/images/carbon_intensity_forecast.png"
      alt="Carbon intensity forecast chart"
      class="segment-image"
    />
    <p>The Carbon Intensity Forecast widget makes time-shifting really simple: it shows how “clean” or “dirty” the grid is expected to be throughout the day,
so you can move flexible electricity use into the greenest hours. The line chart plots the forecast carbon intensity in gCO₂/kWh,
and features like the shaded working-day window and the highlighted “Best 3h window” help you quickly spot when emissions will be lowest.
By scheduling things like EV charging, washing machines, dishwashers, or data-heavy computing tasks into those low-carbon periods—and avoiding the higher peaks at the edges of the day—
you keep your lifestyle the same but reduce the emissions associated with your electricity use.</p>
    </section>
  </article>

  <!-- Carbon Footprint Segment Content -->
<article class="segment segment-footprint">
  <h2>Carbon Footprint</h2>

  <section>
    <h3>Potential impact</h3>
    <p>The GitHub-style carbon footprint heatmap shows a whole year of activity at a glance by representing each day as a small square in a calendar grid, 
just like the familiar commit history view on GitHub. Instead of counting code commits, each square encodes the total carbon footprint from Ada workspace usage on that day. 
The colour ranges from green (low carbon footprint) through orange to red (high carbon footprint), so long stretches of red quickly reveal periods of heavy or wasteful usage,
while greener patches indicate days where users either ran fewer workloads, chose smaller machine sizes, made good use of time-shifting, or switched off idle workspaces.
Because it aggregates both busy and idle usage into a simple visual summary, the heatmap lets users intuitively see how their decisions over the year add up for the planet,
and highlights how much cleaner things could look if they reduced unnecessary idle time and avoided overprovisioning.</p>
    <!-- you can add 2–3 more short sentences from your spec -->
  </section>

  <section>
    <h3>Today’s usage</h3>
    <img
      src="/images/actual_github_commit_history_style_carbon_footprint_heatmap.png"
      alt="Actual carbon footprint heatmap"
      class="segment-image"
    />
  </section>

  <section>
    <h3>If we reduce idle & right-size machines</h3>
    <img
      src="/images/idealised_github_commit_history_style_carbon_footprint_heatmap.png"
      alt="Idealised carbon footprint heatmap"
      class="segment-image"
    />
  </section>
</article>

  </main>
</template>

<script setup>
// Static poster, no js needed
</script>

<style scoped>
.poster {
  /* center the poster on screen */
  margin: 2rem auto;
  background: white;
  box-shadow: 0 0 20px rgba(0,0,0,0.1);

  /* responsive width, let height grow with content */
  width: 100%;
  max-width: 840px;

  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}


/* Print: use full page */
@page {
  size: A0 portrait;
  margin: 0;
}

@media print {
  .poster {
    box-shadow: none;
    margin: 0;
    width: 100%;
    height: auto;
    padding: 40mm;
  }
}

/* Title Row Styles */
.poster-header {
  display: grid;
  grid-template-columns: 1fr 3fr 1.2fr;
  align-items: center;
  gap: 16px;
}

.poster-header img {
  max-width: 100%;
  height: auto;
}

.poster-header h1 {
  font-size: 28px;
  line-height: 1.2;
  margin: 0;
}

.poster-header .name {
  font-weight: 600;
  font-size: 18px;
  margin-bottom: 4px;
}

.poster-header .email {
  font-size: 14px;
  color: #555;
}

/* Layout for sections */

.abstract, .equation {
  border-radius: 16px;
  padding: 16px 20px;
  background: #f7f7f7;
}

.abstract h2,
.equation h2 {
  margin-top: 0;
  font-size: 20px;
}

.segments {
  display: flex;          /* use flexbox instead of grid */
  flex-direction: column; /* stack children vertically */
  gap: 16px;              /* space between rows */
}

.segment {
  border-radius: 16px;
  padding: 12px 14px;
  display: flex;
  flex-direction: column;
  gap: 6px;
  color: #fff;
}


/* Segment Colour Coding*/
.segment-electricity { background: #2b87ff; }  /* blue */
.segment-intensity   { background: #e64141; }  /* red */
.segment-footprint   { background: #2da863; }  /* green */

/* Headings inside colored blocks */
.segment h2 {
  font-size: 18px;
  margin: 0 0 4px;
}
.segment h3 {
  font-size: 14px;
  margin: 8px 0 4px;
}
.segment p, .segment li {
  font-size: 13px;
  line-height: 1.3;
}


/* Electricity Segment Styles */
.inline-logo img {
  max-width: 80px;
  height: auto;
  display: block;
  margin-bottom: 4px;
}

.segment-image {
  max-width: 80%;
  height: auto;
  border-radius: 10px;
  margin: 8px auto;
  background: white;      /* so charts sit on a white card */
  padding: 4px;
  object-fit: contain;
}

/* Carbon Intensity Segment Styles */
.inline-logo-img {
  max-width: 90px;
  margin-bottom: 4px;
}

/* General text styles */
.poster p, .poster li {
  line-height: 1.4;
}

</style>