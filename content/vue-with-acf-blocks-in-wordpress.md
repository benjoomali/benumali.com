---
title: How I use Vue with ACF Blocks in Wordpress
date: 2022-2-22
author: Ben Umali
description: My workflow when building Wordpress themes with Vue and ACF.
tags: ['vue', 'wordpress', 'acf', 'gutenberg']
---

# How I use Vue with ACF Blocks in Wordpress

I found a nifty way to "sprinkle" Vue into my Wordpress themes while mainting the Gutenberg block format. This comes with some challenges and tradeoffs, but fits my workflow when trying to mock and develop websites quickly.

Wrap the inner body with an id of “app”. This allows me to call on Vue components directly in my template files.

```php
<main id="app" class="min-h-screen">
	<!-- Content -->
</main>
```

Then initialize the Vue wrapper in main.js.

```jsx
new Vue({
  el: '#app',
})
```

You can call the components like so

```jsx
Vue.component(
  'ButtonRequestConsultation',
  require('./vue/components/buttonRequestConsultation.vue').default
)
```

I wanted to stick with the Gutenberg process as this is what the core team wanted to move forward with, but couldn’t find an easy way to use Gutenberg with Vue (most were React). So I used [ACF Blocks](https://www.advancedcustomfields.com/resources/blocks/) as a way to create the blocks and wrapped those in Vue components to build a dynamic experience.

Register the block in functions.php (or in my case acfblocks.php)

```php
acf_register_block_type(array(
        'name'              => 'cta_brand_panel_with_image',
        'title'             => __('CTA Brand Panel with Image'),
        'description'       => __('CTA with side by side image. Colors can be adjusted'),
        'render_template'   => 'template-parts/blocks/cta/brand-panel-with-image.php',
        'category'          => 'common',
        'icon'              => 'media-text',
        'keywords'          => array( 'cta','simple','centered', 'buttons' ),
    ));
```

Render a template

```php
<!-- template-parts/blocks/cta/brand-panel-with-image.php -->

<?php
/**
 * Block Name: CTA Brand Panel with Image
 *
 * This is the template that displays the CTA centered. Built on ACF with flexible content:
 * Fields:
 */

$header = get_field('header');
$subheader = get_field('subheader');
$image = get_field('image');

?>

<div class="bg-white">
	<v-lazy-image src="<?php echo $image ?>" alt=""></v-lazy-image>
	<h2 class="text-3xl">
	  <span class="block"><?php echo $header ?></span>
  </h2>
  <p class=""><?php echo $subheader ?></p>
  <div class="w-full md:w-auto mt-8">
			<ButtonRequestConsultation></ButtonRequestConsultation>
   </div>
</div>
```

Since each ACF block was registered relative to the template file, you can call those ACF variables and pass them in as props to your Vue components.

![blocks-in-editor](/blog/blocks-in-editor.png)
