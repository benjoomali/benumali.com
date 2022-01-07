<template>
  <article>
    <Nav />
    <div
      class="max-w-5xl mx-auto w-full mt-5 lg:py-5 px-4 md:px-6 lg:px-8 relative flex flex-col md:items-center"
    >
      <h1
        class="font-semibold text-3xl md:text-4xl lg:text-5xl text-gray-800 md:text-center"
      >
        {{ post.title }}
      </h1>
      <time class="text-blue font-serif text-xl md:text-2xl mt-4 block">{{
        formatDate(post.date)
      }}</time>
    </div>
    <nuxt-content
      :document="post"
      class="prose lg:prose-lg xl:prose-2xl mx-auto mt-5 pb-16 px-4 md:px-6 lg:px-8"
    />
    <Contact />
    <Footer />
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
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'short', day: 'numeric' }
      return new Date(date).toLocaleDateString('en-US', options)
    },
  },
}
</script>
