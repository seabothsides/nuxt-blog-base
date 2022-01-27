<script>
export default {
  layout: 'blog',
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

<template>
  <div>
    <ul>
      <li v-for="link of article.toc" :key="link.id">
        <a :href="`#${link.id}`">
          {{ link.text }}
        </a>
      </li>
    </ul>
    <div>
      <h2>
        {{ article.title }}
      </h2>
      <p>
        {{ formatDate(article.updatedAt) }}
      </p>
      <p>
        {{ article.description }}
      </p>
      <img :src="article.author.img" alt="" />
      <p>
        {{ article.author.name }}
      </p>
      <nuxt-content :document="article" />
    </div>
  </div>
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

code[class*='language-'] ::selection,
code[class*='language-']::selection,
pre[class*='language-'] ::selection,
pre[class*='language-']::selection {
  background: #7e7d7e;
}
.v-application code {
  background-color: transparent;
  color: #f5f7fa;
  font-size: 0.95em;
}

.nuxt-content-highlight .filename {
  color: #cbd5e0;
  z-index: 10;
  position: absolute;
  right: 0;
  margin-right: 0.5rem;
  font-size: 0.865rem;
  font-weight: 300;
  margin-top: 0.25rem;
}

.nuxt-content pre {
  position: static;
  background-color: #2f495e;
}

a {
  text-decoration: none;
}
</style>