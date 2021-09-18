<template>
  <div class="relative block">
    <div class="relative overflow-hidden">
      <Nav />

      <main>
        <div class="pt-10 bg-blue sm:pt-16 lg:pt-8 lg:overflow-hidden">
          <div
            class="mx-auto max-w-7xl lg:px-8 pb-16 sm:pb-44 md:pb-40 lg:pb-0"
          >
            <div class="lg:grid lg:grid-cols-2 lg:gap-8">
              <div
                class="
                  mx-auto
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
                      font-extrabold
                      text-white
                      sm:mt-5 sm:text-6xl
                      lg:mt-6
                      xl:text-6xl
                    "
                  >
                    <span class="block">Hey! I'm</span>
                    <span class="block text-orange">Ben Umali</span>
                  </h1>
                  <p
                    class="
                      mt-3
                      text-base text-gray-100
                      sm:mt-5 sm:text-xl
                      lg:text-lg
                      xl:text-xl
                    "
                  >
                    I'm a Web Developer living in Los Angeles. I'm passionate
                    about building responsive web apps and web sites that drive
                    a great user experience.
                  </p>
                  <p
                    class="
                      mt-3
                      text-base text-gray-100
                      sm:mt-5 sm:text-xl
                      lg:text-lg
                      xl:text-xl
                    "
                  >
                    I cofounded a startup - a SaaS platform built in the
                    property management space to help streamline the move-in
                    process for property managers and their new tenants.
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
              <div class="mt-12 -mb-16 sm:-mb-48 lg:m-0 lg:relative">
                <div
                  class="
                    mx-auto
                    max-w-md
                    px-4
                    sm:max-w-2xl sm:px-6
                    lg:max-w-none lg:px-0
                  "
                >
                  <img
                    class="
                      w-full
                      lg:absolute
                      lg:inset-y-0
                      lg:left-[-100px]
                      lg:h-full
                      lg:w-auto
                      lg:max-w-none
                    "
                    src="~assets/undraw_Coding_re_iv62.svg"
                    alt=""
                  />
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
