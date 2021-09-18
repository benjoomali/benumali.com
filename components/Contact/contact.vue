<template>
  <section id="contact-me" class="overflow-hidden">
    <!-- Contact section -->
    <section
      class="
        relative
        bg-gray-50
        pt-16
        pb-20
        px-4
        sm:px-6
        lg:pt-24 lg:pb-28 lg:px-8
      "
      aria-labelledby="contact-heading"
    >
      <div class="text-center pb-8">
        <h2
          class="
            text-3xl
            tracking-tight
            font-extrabold
            text-white
            md:text-5xl
            xl:text-5xl
          "
        >
          <span class="block text-blue">Get in Touch</span>
        </h2>
        <p class="mt-3 max-w-2xl mx-auto text-xl text-gray-500 sm:mt-4">
          Drop me a line and let's chat!
        </p>
      </div>
      <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="relative bg-white shadow-xl">
          <h2 id="contact-heading" class="sr-only">Contact us</h2>

          <div class="grid grid-cols-1 lg:grid-cols-2">
            <!-- Contact form -->
            <div class="py-10 px-6 sm:px-10 lg:col-span-2 xl:p-12">
              <h3 class="text-lg font-medium text-gray-900">Contact me</h3>
              <form
                data-netlify="true"
                method="POST"
                class="mt-6 grid grid-cols-1 lg:grid-cols-2 gap-y-6 sm:gap-x-8"
              >
                <div>
                  <label
                    for="name"
                    class="block text-sm font-medium text-gray-900"
                    >Name</label
                  >
                  <div class="mt-1">
                    <input
                      id="name"
                      type="text"
                      name="name"
                      autocomplete="given-name"
                      class="
                        py-3
                        px-4
                        block
                        w-full
                        shadow-sm
                        text-gray-900
                        focus:ring-teal-500 focus:border-teal-500
                        border-gray-300
                        rounded-md
                      "
                    />
                  </div>
                </div>
                <div class="hidden">
                  <label
                    >Don’t fill this out if you’re human:
                    <input name="bot-field"
                  /></label>
                </div>
                <div>
                  <label
                    for="email"
                    class="block text-sm font-medium text-gray-900"
                    >Email</label
                  >
                  <div class="mt-1">
                    <input
                      id="email"
                      name="email"
                      type="email"
                      autocomplete="email"
                      class="
                        py-3
                        px-4
                        block
                        w-full
                        shadow-sm
                        text-gray-900
                        focus:ring-teal-500 focus:border-teal-500
                        border-gray-300
                        rounded-md
                      "
                    />
                  </div>
                </div>
                <div class="sm:col-span-2">
                  <div class="flex justify-between">
                    <label
                      for="message"
                      class="block text-sm font-medium text-gray-900"
                      >Message</label
                    >
                    <span id="message-max" class="text-sm text-gray-500"
                      >Max. 500 characters</span
                    >
                  </div>
                  <div class="mt-1">
                    <textarea
                      id="message"
                      name="message"
                      rows="4"
                      class="
                        py-3
                        px-4
                        block
                        w-full
                        shadow-sm
                        text-gray-900
                        focus:ring-teal-500 focus:border-teal-500
                        border border-gray-300
                        rounded-md
                      "
                      aria-describedby="message-max"
                    ></textarea>
                  </div>
                </div>
                <div class="sm:col-span-2 sm:flex sm:justify-end">
                  <button
                    type="submit"
                    class="
                      mt-2
                      w-full
                      inline-flex
                      items-center
                      justify-center
                      px-6
                      py-3
                      border border-transparent
                      rounded-md
                      shadow-sm
                      text-base
                      font-medium
                      text-white
                      bg-blue
                      hover:bg-light_blue
                      focus:outline-none
                      focus:ring-2
                      focus:ring-offset-2
                      focus:ring-light_blue
                      sm:w-auto
                    "
                  >
                    Submit
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
  </section>
</template>
