<template>
  <div>
    <div>
      <div>
        <div v-for="(articles, index) in articles" :key="index">
          <nuxt-link
            :to="{ name: 'blog-slug', params: { slug: articles.slug } }"
          >
            {{ articles.title }}
          </nuxt-link>
          <p>
            {{ articles.description }}
          </p>
        </div>
      </div>
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