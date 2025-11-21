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
  <p>…your abstract text…</p>
  </section>

  <section class="equation">
    <h2>Carbon Footprint Equation</h2>
    <p>Electricity (kWh) × Carbon Intensity (gCO₂eq/kWh) = Carbon Footprint (gCO₂eq)</p>
  </section>

  <section class="segments">
    <article class="segment segment-electricity">
      <!-- electricity content -->
    </article>

    <article class="segment segment-intensity">
      <!-- carbon intensity content -->
    </article>

    <article class="segment segment-footprint">
      <!-- carbon footprint content -->
    </article>
  </section>

  <article class="segment segment-electricity">
  <h2>Electricity</h2>

  <section>
    <h3>How do we get this data?</h3>
    <div class="inline-logo">
      <img src="/images/prometheus_logo.png" alt="Prometheus" />
    </div>
    <ul>
      <li>Pull <code>node_cpu_seconds_total</code> from Ada’s Prometheus database.</li>
      <!-- add your other bullets: idle/busy, 12 W vs 1 W, estimate kWh -->
    </ul>
  </section>

  <section>
    <h3>What does this data show us?</h3>
    <p>Idle vs busy electricity usage in ISIS workspaces.</p>
    <img
      src="/images/estimated_usage_bar_chart.png"
      alt="Idle vs busy electricity usage chart"
      class="segment-image"
    />
    <!-- add your “~60% idle”, Zombie VMs, etc. as short bullet points -->
  </section>

  <section>
    <h3>How can we use this to reduce carbon footprint?</h3>
    <p>Highlight wasteful idle usage and encourage users to shut down workspaces.</p>
    <img
      src="/images/workspace_tracker.png"
      alt="Workspace tracker UI"
      class="segment-image"
    />
    <!-- add 1–2 bullets about workspace tracker & upfront costing -->
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

  /* approximate A0 portrait ratio */
  width: 840px;         /* pick any width you like */
  height: calc(840px * 1.414); /* ≈ A-series portrait ratio */

  padding: 40px;
  display: flex;
  flex-direction: column;
  gap: 24px;
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
  flex: 1; /* take remaining height */
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.segment {
  border-radius: 16px;
  padding: 16px 14px;
  display: flex;
  flex-direction: column;
  gap: 8px;
  color: #fff;
}

/* Color coding to direct the eye */
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
  width: 100%;
  border-radius: 10px;
  margin: 6px 0;
  background: white;      /* so charts sit on a white card */
  padding: 4px;
}

</style>