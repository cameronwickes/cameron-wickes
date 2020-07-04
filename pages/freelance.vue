<template>
  <div id="freelance-page" class="page-wrapper freelance-page content-page">
    <site-hero
      title="Freelance"
      subtitle="Need help with a project?"
      image="/uploads/aboutmefinal.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
        <div class="content">
          <h3>Freelance Work</h3>
          <p>Need help designing a website? Have an old computer that needs upgrading? You're in the right place. I offer a range of technical services including but not limited to:</p>
          <ul>
          <li>Graphic Design</li>
          <li>Website Development</li>
          <li>Computer Hardware Upgrades</li>
          </ul>
          <p>Please get in touch to discuss specific requirements, and find out what I can do for you!</p>
          <p>enquiries@cameronwickes.com</p>
          <p>Thank you!</p>
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
