<template>
  <div id="categories-page" class="page-wrapper categories-page">
    <site-hero 
    title="Categories" 
    subtitle="Pick a topic to see relevant articles"
    image="/uploads/categoriesfinal.jpg" />
    <main-section theme="one-column">
      <categories-grid />
    </main-section>
  </div>
</template>
<script>
export default {
  head() {
    return {
      title: `Categories | ${this.$siteConfig.siteName}`
    }
  }
}
</script>
