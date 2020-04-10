<template>
  <div id="about-page" class="page-wrapper about-page content-page">
    <site-hero
      title="About Me"
      subtitle="A little bit about myself..."
      image="/uploads/aboutmefinal.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
        <div class="content">
          <h>Hi!<h>
          <p>I am Cameron Wickes, a 17 year old student from Cumbria, with a love for Cybersecurity and all things Computer Science.<p>
          <p>I am interested in all sorts of areas, and am always trying to expand my knowledge of the subject. </p>
          <p>This blog serves as a space to share and collate my personal learning experiences as I progress in the field, in the hopes to provide a knowledge bank for up and coming enthusiasts.</p>
          <p>Click on some other sections to explore more!</p>
        </div>
      </template>

      <template v-slot:sidebar>
        <h3 class="subtitle is-4">
          Latest Posts
        </h3>
        <posts-grid :per-row="1" :number="2" />
      </template>
    </main-section>
  </div>
</template>
<script>
import QuoteCard from '~/components/cards/QuoteCard'
export default {
  head() {
    return {
      title: `About | ${this.$siteConfig.siteName}`
    }
  },
  components: { QuoteCard }
}
</script>
