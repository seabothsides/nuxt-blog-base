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
  <div class="px-8 grid gap-6 place-content-center md:px-44 h-full">
    <div
      v-for="(i, index) in landing.section"
      :key="index"
      class="p-2 grid grid-flow-rows gap-4"
    >
      <p class="font-bold text-xl">
        {{ landing.section[index].content.title }}
      </p>
      <p>
        {{ landing.section[index].content.caption }}
      </p>
      <nuxt-link
        v-if="landing.section[index].content.button.iurl"
        :to="{ name: landing.section[index].content.button.iurl }"
        class="
          place-self-center
          border border-4
          rounded-md
          p-1.5
          border-green-400
          capitalize
          transition
          duration-200
          ease-out
          hover:ease-in
          hover:bg-gradient-to-r
          hover:text-white
          hover:font-bold
          hover:from-green-300
          hover:to-blue-400
        "
      >
        {{ landing.section[index].content.button.name }}
      </nuxt-link>
      <a
        v-if="landing.section[index].content.button.eurl"
        :href="landing.section[index].content.button.eurl"
        target="_blank"
        class="
          place-self-center
          border border-4
          rounded-md
          p-1.5
          border-green-400
          capitalize
          transition
          duration-200
          ease-out
          hover:ease-in
          hover:bg-gradient-to-r
          hover:text-white
          hover:font-bold
          hover:from-green-300
          hover:to-blue-400
        "
      >
        {{ landing.section[index].content.button.name }}
      </a>
      <img
        class="rounded-3xl order-first"
        :src="landing.section[index].content.image"
        alt=""
      />
    </div>
  </div>
</template>


<style lang="sass" scoped>
a
  text-decoration: none
</style>
