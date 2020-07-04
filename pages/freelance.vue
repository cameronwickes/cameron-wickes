<template>
  <div id="freelance-page" class="page-wrapper freelance-page content-page">
    <site-hero
      title="Freelance"
      subtitle="A little bit about myself..."
      image="/uploads/aboutmefinal.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
        <div class="content">
          <h3>Hi!</h3>
          <p>I’m Cameron Wickes, an 18-year-old student from Cumbria, with a love for computers and information security.</p>
          <p>My journey into infosec started a couple of years ago, when a friend introduced me to an online cybersecurity course. Having loved Computer Science throughout my seven years at secondary school, I immediately jumped at the idea had completed the course within a couple of days.</p>
          <p>I am always trying to expand my knowledge of the subject, in whatever form that may be, but I am particularly interested in developing areas such as User Behaviour and Entity Analytics, or Malware Analysis using Machine Learning. I find this stuff really cool!</p>
          <p>Python is my go-to programming language, due to its flexibility and speed, but I have a background in VB.NET, and am currently learning C. I enjoy solving problems with a creative approach, which is why the unlimited possibilities of coding appeal to me, but cybersecurity also allows me to delve into advanced theoretical and academic topics, which I find highly stimulating.</p>
          <p>Through HMG and the SANS institute, I got the chance to participate in and complete the SANS SEC504 course, which I enjoyed thoroughly. I hope to get the chance to participate in more events like these over the coming years.</p>
          <p>This blog serves as a space to share and collate my personal learning experiences as I progress in the field, in the hopes to provide a space where up and coming enthusiasts can find relevant material.</p>          
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
      title: `About | ${this.$siteConfig.siteName}`
    }
  },
  components: { QuoteCard }
}
</script>
