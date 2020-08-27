<template>
  <div id="home-page" class="page-wrapper home-page">
    <meta property='og:title' content='Cameron Wickes'/>
    <meta property='og:image' content='https://cameron-wickes-blog.s3.eu-west-2.amazonaws.com/favicon.png'/>
    <meta property='og:description' content='Personal Website'/>
    <meta property='og:url' content='https://www.cameronwickes.com/'/>
    <site-hero :title="title" :subtitle="subtitle" :image="featureImage">
    <button
        class="button is-primary"
        @click="$router.push('/about')" 
      >
        Find out more...
      </button>
    </site-hero>
    <main-section theme="one-column">
      <template v-slot:default>
        <!-- All Posts -->
        <posts-grid />
      </template>
      <template v-slot:sidebar>
        Nothing here
      </template>
    </main-section>
    <news-letter-form-modal />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { setPageData } from '../helper'
import NewsLetterFormModal from '~/components/NewsLetterFormModal'

export default {
  name: 'HomePage',
  head() {
    return {
      title: `Home | ${this.$siteConfig.siteName}`
    }
  },
  components: {
    NewsLetterFormModal
  },
  computed: {
    ...mapState(['title', 'subtitle', 'featureImage'])
  },
  fetch({ store, params }) {
    setPageData(store, { slug: 'home' })
  }
}
</script>

<style>
.home-page .under-subtitle {
  border-top: none;
}
</style>
