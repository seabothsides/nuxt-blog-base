<script>
export default {
  data() {
    return {}
  },
  async asyncData({ $content, params }) {
    const landing = await $content('pages/landing').fetch()

    return { landing }
  },
  head() {
    return {
      title: this.landing.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.landing.description,
        },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.landing.title },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.landing.description,
        },
        // Twitter Card
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: this.landing.title,
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.landing.description,
        },
      ],
    }
  },
}
</script>

<template>
  <div>
    <div v-for="(i, index) in landing.section" :key="index">
      <p>
        {{ landing.section[index].content.title }}
      </p>
      <p>
        {{ landing.section[index].content.caption }}
      </p>
      <nuxt-link
        v-if="landing.section[index].content.button.eurl"
        :to="{ name: landing.section[index].content.button.eurl }"
      >
        {{ landing.section[index].content.button.name }}
      </nuxt-link>
      <a
        v-if="landing.section[index].content.button.iurl"
        :href="landing.section[index].content.button.iurl"
        target="_blank"
      >
        {{ landing.section[index].content.button.name }}
      </a>
      <img :src="landing.section[index].content.image" alt="" />
    </div>
  </div>
</template>


<style lang="sass" scoped>
a
  text-decoration: none
</style>
