<template>
  <div id="contact-page" class="page-wrapper contact-page content-page">
    <site-hero
      title="Contact Me"
      subtitle="Get in touch!"
      image="/uploads/contact.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
       <div class="content">
           <h3 style="text-align:center">Thanks for contacting... I will be in touch as soon as possible!</h3>
       </div>
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
