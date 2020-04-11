<template>
  <div id="contact-page" class="page-wrapper contact-page content-page">
    <site-hero
      title="Contact Me"
      subtitle="Get in touch!"
      image="/uploads/contact.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
      <h3>Thanks for contacting! I will get back to you as soon as possible!</h3>
      <br>
      </template>
      <template v-slot:sidebar>
        <h3 class="subtitle is-4">
          Latest Posts
        </h3>
        <!-- Latest Posts -->
        <posts-grid :per-row="1" :number="2" />
      </template>
    </main-section>
  </div>
</template>
<script>

export default {
  head() {
    return {
      title: `Success | ${this.$siteConfig.siteName}`
    }
  },
}
</script>
