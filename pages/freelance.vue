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
          <h3>Hi!</h3>
          <p>I’m Cameron Wickes, an 18-year-old student from Cumbria, with a love for computers and information security.</p>
          <h3>Contact Me</h3>
            <p>If you'd like to get in touch with me, please do so via one of the methods below:</p>
            <font-awesome-icon :icon="{prefix: 'fab',iconName: 'twitter'}" size="3x" style="vertical-align:middle" />
            <a style="font-size:20px; font-weight:bold; vertical-align:middle; color:#09b4ed" href="https://twitter.com/cameronjwickes" target="_blank">   Twitter</a>
            <br>
            <font-awesome-icon :icon="{prefix: 'fab',iconName: 'linkedin'}" size="3x" style="vertical-align:middle" />
            <a style="font-size:20px; font-weight:bold; vertical-align:middle; color:#09b4ed" href="https://www.linkedin.com/in/cameron-wickes-7b32aa192/" target="_blank">    LinkedIn</a>
            <br>
            <font-awesome-icon icon="envelope" size="3x" style="vertical-align:middle"/>
            <span style="font-size:20px; font-weight:bold; vertical-align:middle; color:#09b4ed">   enquiries@cameronwickes.com</span> 
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
