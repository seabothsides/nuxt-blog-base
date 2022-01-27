<template>
  <div class="grid grid-auto-row gap-3">
    <div
      v-for="(articles, index) in articles"
      :key="index"
      class="p-2 border rounded-lg border-4 border-gray-400"
    >
      <nuxt-link
        :to="{ name: 'blog-slug', params: { slug: articles.slug } }"
        class="font-semibold hover:underline"
      >
        {{ articles.title }}
      </nuxt-link>
      <p class="font-light">
        {{ articles.description }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'blog',
  async asyncData({ $content }) {
    const articles = await $content('blog').sortBy('createdAt', 'desc').fetch()

    return { articles }
  },
}
</script>

<style lang="sass" scoped>
ul
  list-style: none
a
  text-decoration: none
</style>