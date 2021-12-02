<template>
  <div class="relative block min-h-screen">
    <HeroSmall />
    <div class="max-w-7xl mx-auto px-4 md:px-6 lg:px-8">
      <ul class="py-10 max-w-4xl">
        <li v-for="link of posts" :key="link.id" class="mb-6 group">
          <NuxtLink :to="'blog' + link.path">
            <div class="p-8">
              <h3
                class="
                  text-2xl
                  font-semibold
                  text-gray-900
                  group-hover:text-light_blue
                "
              >
                {{ link.title }}
              </h3>
              <p class="hidden group-hover:text-blue">{{ link.date }}</p>
              <p
                class="mt-3 text-base text-gray-500 group-hover:text-light_blue"
              >
                {{ link.description }}
              </p>
            </div>
          </NuxtLink>
        </li>
      </ul>
    </div>
    <Contact />
    <Footer />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    try {
      const posts = await $content({ deep: true })
        .only(['title', 'description', 'image', 'path', 'date'])
        .sortBy('date', 'desc')
        .fetch()
      return { posts }
    } catch (err) {}
  },
}
</script>

<style></style>
