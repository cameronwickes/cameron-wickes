<template>
  <div id="categories-page" class="page-wrapper categories-page">
    <site-hero title="Categories" image="https://cdn.pixabay.com/photo/2015/02/24/15/41/dog-647528__340.jpg" />
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
