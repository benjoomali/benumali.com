<template>
  <div class="flex flex-col rounded-lg shadow-lg overflow-hidden">
    <div class="flex-shrink-0">
      <img
        class="h-48 md:h-64 lg:h-80 w-full object-cover object-top"
        :src="require(`~/assets/${project.image}`)"
        alt=""
      />
    </div>
    <div class="flex-1 bg-white p-6 flex flex-col justify-between">
      <div class="flex-1">
        <p class="text-sm font-medium text-indigo-600">
          {{ project.workType }}
        </p>
        <a :href="project.anchor" class="block mt-2 group">
          <p
            class="text-xl font-semibold text-blue group-hover:text-light_blue"
          >
            {{ project.title }}
          </p>
          <p class="mt-3 text-base text-gray-500">
            {{ project.description }}
          </p>
        </a>
      </div>
      <div class="mt-6 flex items-center">
        <div class="relative">
          <div
            v-if="project.techStack"
            class="flex justify-start flex-wrap text-sm text-gray-500 overflow-x-auto"
          >
            <span
              v-for="tech in project.techStack"
              :key="tech"
              class="inline-flex items-center mr-2 mt-1 px-2.5 py-0.5 rounded-md text-sm font-medium bg-gray-100 text-gray-800 whitespace-nowrap"
            >
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
}
</script>
