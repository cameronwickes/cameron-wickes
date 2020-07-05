<template>
  <div id="freelance-page" class="page-wrapper freelance-page content-page">
    <site-hero
      title="Freelance"
      subtitle="Need help with a project?"
      image="/uploads/freelance.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
        <div class="content">
          <h3>What can I help you with?</h3>
          <p>Need help designing a website? Have an old computer that needs upgrading?</p>
          <p>I offer a range of technical services including but not limited to:</p>
          <ul>
          <li>Graphic Design</li>
          <li>Website Development</li>
          <li>App Development</li>
          <li>Computer Hardware Upgrades</li>
          </ul>
          <p>If you have a project that you'd like me to be a part of, want to see if I offer a service or want to discuss specific requirements, please get in touch at <span style='color:#09b4ed'>enquiries@cameronwickes.com.</span>
          <p>Thank you!</p>
          <h3>Recent Projects</h3>
          
          <h3>Testimonials</h3>
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
      title: `Freelance | ${this.$siteConfig.siteName}`
    }
  },
  components: { QuoteCard }
}
</script>
