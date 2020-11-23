<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('blog', params.slug).fetch()

    return { article }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    },
  },
  head() {
    return {
      title: this.article.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.article.description,
        },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.article.title },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.article.description,
        },
        // Twitter Card
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: this.article.title,
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.article.description,
        },
      ],
    }
  },
}
</script>

<template lang="pug">
v-container
  v-navigation-drawer(right, clipped, app)
    ul
      p.text-center.overline.mb-n1 Table Of Contents
      li(v-for="link of article.toc" :key="link.id" :class="{ 'text-wrap pb-1 v-list-item__title': link.depth === 2, 'pl-5 pb-1 v-list-item__subtitle': link.depth === 3 }")
        NuxtLink(:to="`#${link.id}`") {{ link.text }}
  v-container
    h1.text-h4.text-capitalize {{ article.title }}
    div.text-overline.ml-1.text--secondary Article last updated: {{ formatDate(article.updatedAt) }}
    div.text-subtitle-1 {{ article.description }}
    v-card.pa-1.align-center.mb-1(flat)
      v-avatar.mr-2 
        img( :src="article.author.img" )
      p.d-inline.subtitle-2.text--secondary Author: {{ article.author.name }}
    v-divider
    ul.hidden-md-and-up.mb-2.pl-2
      p.text--secondary.mb-n1.overline Table Of Contents
      li.mb-1(v-for="link of article.toc" :key="link.id" :class="{ 'text-wrap v-list-item__title': link.depth === 2, 'pl-5 v-list-item__subtitle': link.depth === 3 }")
        NuxtLink(:to="`#${link.id}`") {{ link.text }}
    v-divider.mb-2
    nuxt-content(:document="article") /
</template>

<style>
.nuxt-content h2 {
  margin-bottom: 0.25em;
  margin-top: 1.75em;
}

.nuxt-content strong {
  color: #e040fb;
}

.nuxt-content a {
  text-decoration: none;
  color: #3d5afe;
}

.nuxt-content li {
  margin-bottom: 0.75em;
}

.nuxt-content blockquote {
  background: #f6fbfb;
  border-left: 10px solid #1460b6;
  color: #1460b6;
  margin: 1.5em 10px;
  padding: 0.5em 10px;
}

.v-application code {
  background-color: #e3edf2;
  color: #1460b6;
  font-size: 1em;
}

pre[class*='language-'] {
  background: #f6fbfb;
}

a {
  text-decoration: none;
}
</style>