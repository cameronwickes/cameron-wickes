<template>
  <div id="categories-page" class="page-wrapper categories-page">
    <site-hero title="Categories" image="uploads/maarten-van-den-heuvel-8EzNkvLQosk-unsplash.jpg" />
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
