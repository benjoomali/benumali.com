<template>
  <main class="antialiased text-gray-900">
    <section class="relative block min-h-screen">
      <Hero />
      <About />
      <Work />
      <Contact />
      <Footer />
    </section>
  </main>
</template>

<script>
import Hero from '~/components/Hero/hero.vue'
import Work from '~/components/Work/work.vue'
import Contact from '~/components/Contact/contact.vue'
import Footer from '~/components/Footer/footer.vue'
export default {
  components: {
    Hero,
    Work,
    Contact,
    Footer,
  },
}
</script>

<style>
html {
  scroll-behavior: smooth;
}
</style>
