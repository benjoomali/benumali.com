<template>
  <header class="relative">
    <div class="bg-blue py-6">
      <nav
        class="relative max-w-7xl mx-auto flex items-center justify-between px-4 sm:px-6"
        aria-label="Global"
      >
        <div class="flex items-center flex-1">
          <div class="flex items-center justify-between w-full md:w-auto">
            <NuxtLink to="/">
              <span
                class="uppercase text-2xl font-bold text-white hover:text-orange transition-all ease-in-out duration-150"
                >Ben Umali</span
              >
              <img
                class="hidden h-8 w-auto sm:h-10 text-orange fill-current"
                src="https://tailwindui.com/img/logos/workflow-mark-indigo-500.svg"
                alt=""
              />
            </NuxtLink>
          </div>
          <div class="space-x-8 flex md:ml-10">
            <NuxtLink
              to="/blog"
              class="text-base font-medium text-gray-100 hover:text-orange"
              >Blog</NuxtLink
            >
          </div>
        </div>
      </nav>
    </div>
  </header>
</template>

<style>
a.nuxt-link-active {
  @apply text-orange;
}
/* home route and active route will show in bold as it matches / and /about */
a.nuxt-link-exact-active {
  @apply text-orange;
}
</style>
