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
    <ul class="border-2 p-2 rounded-md shadow-inner shadow-lg">
      <li
        v-for="link of article.toc"
        :key="link.id"
        class="font-semibold hover:underline"
      >
        <a :href="`#${link.id}`">
          {{ link.text }}
        </a>
      </li>
    </ul>
    <div class="py-4">
      <h2 class="font-bold text-2xl">
        {{ article.title }}
      </h2>
      <p class="font-light italic">
        {{ formatDate(article.updatedAt) }}
      </p>
      <p class="font-light">
        {{ article.description }}
      </p>
      <div class="flex pb-3 items-center space-x-4">
        <img class="w-9" :src="article.author.img" alt="" />
        <p>
          {{ article.author.name }}
        </p>
      </div>
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
  color: #3a74cc;
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

.nuxt-content h2 {
  font-weight: 700;
  font-size: 1.35em;
}

a {
  text-decoration: none;
}
</style>