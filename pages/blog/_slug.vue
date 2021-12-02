<template>
  <article>
    <Nav />
    <nuxt-content
      :document="page"
      class="
        prose prose-sm
        sm:prose
        lg:prose-lg
        xl:prose-2xl
        mx-auto
        mt-5
        pt-8
        pb-16
      "
    />
  </article>
</template>

<script>
import Nav from '../../components/Nav/nav.vue'
export default {
  components: { Nav },
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'index'
    const page = await $content(slug).fetch()

    return {
      page,
    }
  },
}
</script>
