<template>
  <nav
    class="px-3 bg-gray-200 md:px-56 md:py-1.5 grid grid-flow-col items-center"
  >
    <p>
      <nuxt-link class="font-bold text-3xl hover:text-green-500" to="/">
        Brand Logo
      </nuxt-link>
    </p>
    <div class="flex justify-around capitalize">
      <nuxt-link
        class="
          transition
          ease-in-out
          duration-200
          text-lg
          font-semibold
          hover:text-red-400
        "
        v-for="link in links"
        :to="{ name: link.link }"
        :key="link.id"
      >
        {{ link.name }}</nuxt-link
      >
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      links: [
        {
          name: 'blog',
          link: 'blog',
        },
        {
          name: 'shop',
          link: 'shop',
        },
      ],
    }
  },
}
</script>