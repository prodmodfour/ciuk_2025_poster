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
</style>