<template>
  <article>
    <Nav />
    <nuxt-content
      :document="post"
      class="prose prose-sm sm:prose lg:prose-lg xl:prose-2xl mx-auto mt-5 pt-8 pb-16 px-4 md:px-6 lg:px-8"
    />
  </article>
</template>

<script>
import Nav from '../../components/Nav/nav.vue'
export default {
  components: { Nav },
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'index'
    const post = await $content(slug).fetch()

    if (!post) {
      return error({ statusCode: 404, message: 'Post not found' })
    }

    return {
      post,
    }
  },
}
</script>
