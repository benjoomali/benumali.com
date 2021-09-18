<template>
  <div class="relative block">
    <div class="relative overflow-hidden">
      <Nav />

      <main>
        <div class="pt-10 bg-blue sm:pt-16 lg:pt-0 lg:overflow-hidden">
          <div class="mx-auto max-w-7xl lg:px-8 pb-16 sm:pb-20 lg:pb-0">
            <div class="lg:grid lg:grid-cols-3 lg:gap-8">
              <div
                class="
                  col-span-2
                  mr-auto
                  max-w-md
                  px-4
                  sm:max-w-2xl sm:px-6 sm:text-center
                  lg:px-0 lg:text-left lg:flex lg:items-center
                "
              >
                <div class="lg:py-16">
                  <h1
                    class="
                      mt-4
                      text-4xl
                      tracking-tight
                      font-extrabold
                      text-white
                      sm:mt-5 sm:text-6xl
                      lg:mt-6
                      xl:text-6xl
                    "
                  >
                    <span class="block text-orange">Blog</span>
                  </h1>
                  <p
                    class="
                      mt-3
                      text-base text-gray-100
                      sm:mt-5 sm:text-xl
                      lg:text-2xl
                    "
                  >
                    Learnings and Lessons
                  </p>
                  <div class="block relative w-auto mt-8">
                    <a
                      href="#contact-me"
                      class="
                        text-xl
                        font-medium
                        rounded-lg
                        bg-orange
                        hover:bg-white
                        text-white
                        hover:text-orange
                        duration-150
                        ease-in-out
                        px-10
                        py-3
                        hover:scale-105
                      "
                    >
                      Get in Touch
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import Nav from '~/components/Nav/nav.vue'
export default {
  components: {
    Nav,
  },
}
</script>
