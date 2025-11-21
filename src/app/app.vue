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

  <div class="top-row">
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
      <p>Carbon Footprint (gCO₂eq) </p>
      <p>=</p>
      <p>Electricity × Carbon Intensity </p>
      <p>(kWh) x (gCO₂eq/kWh)</p>
    </section>
  </div>

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
      <li>Workspace tracker: Implementing a card that shows idle electricity usage and waste carbon emissions.</li>
      <li>Upfront Costing: Display average carbon usage values for each machine size before creation.</li>
    </ul>
    </section>
  </article>

  <article class="segment segment-intensity">
  <h2>Carbon Intensity</h2>

  <section>
    <h3>How do we get this data?</h3>
    <img
      src="/images/carbon_intensity_api_logo.png"
      alt="Carbon Intensity API"
      class="inline-logo-img"
    />
    <ul> The Carbon Intensity API (NESO) provides real-time and forecast data on GB grid carbon intensity. 
    It uses generation mix data (renewables, nuclear, fossil fuels) to allow apps to schedule electricity use during "cleaner" times.
    </ul>
</section>

  <section>
    <h3>What does this data show us?</h3>
    <img
      src="/images/generation_mix.png"
      alt="Generation mix"
      class="segment-image"
    />
    <p>The generation mix breaks down electricity production (wind, solar, gas, etc.). 
    When renewables dominate, intensity drops; when fossil fuels dominate, it rises. This transparency helps users choose low-carbon periods.</p>
  </section>

  <section>
    <h3>How can we reduce footprint?</h3>
    <img
      src="/images/carbon_intensity_forecast.png"
      alt="Carbon intensity forecast chart"
      class="segment-image"
    />
    <p>The Forecast widget enables time-shifting. The line chart and highlighted "Best 3h window" help users schedule heavy computing or other tasks during low-carbon periods, reducing emissions without changing lifestyle.</p>
    </section>
  </article>

  <article class="segment segment-footprint">
  <h2>Carbon Footprint</h2>

  <section>
    <h3>Potential impact</h3>
    <p>The GitHub-style heatmap shows a year of activity. Each square is a day, colored from green (low carbon) to red (high carbon). 
    It visualizes trends, revealing wasteful usage periods (red) versus efficient operations (green), helping users intuitively understand the long-term impact of their computing choices.</p>
  </section>

  <section>
    <h3>Today’s usage</h3>
    <img
      src="/images/actual_github_commit_history_style_carbon_footprint_heatmap.png"
      alt="Actual carbon footprint heatmap"
      class="segment-image"
    />
    <p><i>Current state with heavy idle usage.</i></p>
  </section>

  <section>
    <h3>If we reduce idle & right-size machines</h3>
    <img
      src="/images/idealised_github_commit_history_style_carbon_footprint_heatmap.png"
      alt="Idealised carbon footprint heatmap"
      class="segment-image"
    />
    <p><i>Projected state with optimized resources.</i></p>
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
  max-width: 840px; /* Scaled down A0 representation for screen */

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
    padding: 30mm; 
  }
}

/* Title Row Styles */
.poster-header {
  display: grid;
  grid-template-columns: 1fr 3fr 1.2fr;
  align-items: center;
  gap: 20px;
  margin-bottom: 10px;
}

.poster-header img {
  max-width: 100%;
  height: auto;
}

.poster-header h1 {
  font-size: 28px;
  line-height: 1.1;
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

/* Top Row: Abstract & Equation Side-by-Side */
.top-row {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 16px;
}

.abstract, .equation {
  border-radius: 16px;
  padding: 10px 16px; /* Reduced padding */
  background: #f7f7f7;
}

.abstract h2,
.equation h2 {
  margin-top: 0;
  font-size: 18px;
  margin-bottom: 6px;
  color: #333;
}

.abstract p {
  font-size: 11px; /* Smaller text for abstract */
  line-height: 1.25;
  margin-bottom: 0;
}

.equation {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.equation p {
  font-size: 12px;
  font-weight: 600;
  text-align: center;
  color: #444;
}

/* Segment Container Styles */
.segment {
  border-radius: 16px;
  padding: 16px 20px;
  color: #fff;
  
  /* Grid Layout for shorter vertical height */
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* 3 Equal columns */
  gap: 20px;
  align-items: start;
}

/* Segment Colour Coding*/
.segment-electricity { background: #2b87ff; }  /* blue */
.segment-intensity   { background: #e64141; }  /* red */
.segment-footprint   { background: #2da863; }  /* green */

/* Headings inside colored blocks */
.segment h2 {
  font-size: 22px;
  margin: 0 0 10px;
  
  /* Make the H2 span across the top of the 3 columns */
  grid-column: 1 / -1;
  border-bottom: 1px solid rgba(255,255,255,0.3);
  padding-bottom: 8px;
}

.segment h3 {
  font-size: 16px;
  margin: 0 0 8px;
  font-weight: 600;
  min-height: 40px; /* Ensure alignment across columns */
  display: flex;
  align-items: flex-end;
}

.segment p, .segment li {
  font-size: 12px;
  line-height: 1.35;
}

.segment ul {
  padding-left: 20px;
  margin: 0;
}

/* Image Handling within Grid */
.inline-logo img {
  max-width: 100px;
  height: auto;
  display: block;
  margin-bottom: 8px;
}

.segment-image {
  width: 100%; /* Fill the grid column */
  max-height: 180px; /* Cap height to keep segment short */
  object-fit: contain; /* Don't distort aspect ratio */
  border-radius: 8px;
  margin: 8px 0;
  background: white;
  padding: 6px;
}

.inline-logo-img {
  max-width: 120px;
  background: white;
  padding: 4px;
  border-radius: 4px;
  margin-bottom: 8px;
}

.segment-footprint .segment-image {
  max-height: 220px;
}

/* General text styles */
.poster p, .poster li {
  line-height: 1.4;
}

</style>