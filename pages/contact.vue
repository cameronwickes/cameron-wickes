<template>
  <div id="contact-page" class="page-wrapper contact-page content-page">
    <site-hero
      title="Contact Me"
      subtitle="Get in touch!"
      image="/uploads/contact.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
      <p>If you would like to get in contact with me, please fill in the form below, and I will get back to you as soon as possible!</p>
      <br>
           <contact-form />
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
import ContactForm from '~/components/ContactForm'
export default {
  head() {
    return {
      title: `Contact | ${this.$siteConfig.siteName}`
    }
  },
  components: { ContactForm }
}
</script>
