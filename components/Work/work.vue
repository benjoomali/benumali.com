<template>
  <div
    class="relative bg-gray-50 pt-16 pb-20 px-4 sm:px-6 lg:pt-24 lg:pb-28 lg:px-8"
  >
    <div class="absolute inset-0">
      <div class="bg-white h-1/3 sm:h-2/3"></div>
    </div>
    <div class="relative max-w-7xl mx-auto">
      <div class="text-center">
        <h2
          class="text-3xl tracking-tight font-extrabold text-white md:text-5xl xl:text-5xl"
        >
          <span class="block text-blue">My Work</span>
        </h2>
        <p class="mt-3 max-w-2xl mx-auto text-xl text-gray-500 sm:mt-4">
          A collection of featured work
        </p>
      </div>
      <div
        class="mt-12 max-w-lg md:max-w-3xl mx-auto grid gap-5 md:grid-cols-2 lg:max-w-5xl"
      >
        <Card
          v-for="project in projects"
          :key="project.id"
          :project="project"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Card from '~/components/Work/card.vue'
export default {
  components: {
    Card,
  },
  data() {
    return {
      projects: [
        {
          id: 1,
          workType: 'eCommerce',
          title: 'Hopialikeit.com',
          description:
            'A custom Woocommerce Theme built for a popular Filipino Bakery in the Southern California area. Built with a Custom Cart and Post Types to showcase the different foods and baked goods the restaurant offers.',
          techStack: ['WooCommerce', 'Vue', 'Tailwind', 'CoCart API'],
          image: 'hopia-like-it-screenshots.jpg',
          anchor: 'https://hopialikeit.com',
        },
        {
          id: 2,
          workType: 'Website',
          title: 'Jae Pak MD Medical',
          description:
            'A custom Wordpress Theme developed for a Brentwood based Medical clinic specializing in Hair Restoration.',
          techStack: ['Wordpress', 'Vue', 'Tailwind', 'ACF'],
          image: 'jaepakmd-screenshot.jpg',
          anchor: 'https://jpmdmedical.com',
        },
        {
          id: 3,
          workType: 'Web App',
          title: 'Ultimate Logistics',
          description:
            'A custom CMS built for a Central California Trucking and Logistics Broker to facilitate their sales flow.',
          techStack: [
            'Ruby on Rails',
            'Stimulus',
            'TailwindUI',
            'Algolia Search API',
          ],
          image: 'ul-screenshot.jpg',
          anchor: '',
        },
        {
          id: 4,
          workType: 'SaaS',
          title: 'Getsettledin.com',
          description:
            'I cofounded a (now defunct) Property Management SaaS platform created to help streamline the move-in process for property managers and their new tenants.',
          techStack: ['Ruby on Rails', 'Vue', 'Tailwind'],
          image: 'getsettledin-screenshot.jpg',
          anchor: '',
        },
      ],
    }
  },
}
</script>
