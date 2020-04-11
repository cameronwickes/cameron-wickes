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
          <h3>Hi!</h3>
          <p>I am Cameron Wickes, a 17-year-old student from Cumbria, with a love for Cybersecurity and all things computer-related. My journey started a couple of years ago, when a friend introduced me to a Cybersecurity course. Having loved Computer Science for a while, I immediately jumped at the idea.</p>
          <p>Python is my go-to language, due to it’s flexibility and speed, but I have a background in VB.NET, and am currently learning C.  I love solving problems with a creative approach, which is why coding is such an appeal, but cybersecurity lets me combine this passion for coding with advanced theoreticality. To code well, you need a willingness to change your thinking and work collaboratively with other people. I am very much a people person, and enjoy working in teams, but can also work well individually.</p>
          <p>Through HMG and the SANS institute, I got the chance to participate in and complete the SANS SEC504 course, which I enjoyed thoroughly. I hope to get the chance to participate in more events like these.</p>
          <p>I am always trying to expand my knowledge of the subject, and up and coming areas are what fascinate me the most, such as User Behaviour and Entity Analytics, or Malware Analysis using Machine Learning.</p>
          <p>This blog serves as a space to share and collate my personal learning experiences as I progress in the field, in the hopes to provide a space where up and coming enthusiasts can find relevant material.</p>
          <p>Click on some other sections to explore more!</p>
          <h3>Contact Me</h3>
          <p>If you'd like to get in touch with me, please do so via one of the sites below:</p>
          <font-awesome-icon :icon="{prefix: 'fab',iconName: 'twitter'}" />
          <a href="https://twitter.com/cameronwickes0" target="_blank">Twitter</a>
          <br>
          <font-awesome-icon :icon="{prefix: 'fab',iconName: 'linkedin'}" />
          <a href="https://www.linkedin.com/in/cameron-wickes-7b32aa192/" target="_blank">LinkedIn</a>
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
