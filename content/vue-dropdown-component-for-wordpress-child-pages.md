---
title: Creating a Custom Vue Dropdown Component for Wordpress Child Pages using REST API
date: 2020-01-27
author: Ben Umali
description: So currently I'm building a custom theme in Wordpress that implements Vue with completely replacing the front end. Here's how I build a dropdown component in Vue...
tags: ['vuejs', 'wordpress']
---

## Child Page Dropdown via Wordpress Rest API in Vue

#### January 27, 2020

So currently I'm building a custom theme in Wordpress that implements Vue without completely replacing the front end. The reasoning for this is rooted in SEO and a lot of legacy content, so instead of using Vue Router and the works, I mount Vue components to the Wordpress templates.

![background](/blog/vue-dropdown-open.png)

### The Problem

While building the custom theme, one of the issues I had was that I wanted to showcase a list of links in a dropdown. In my current work, a lot of the pages had links to resources and other articles. More importantly, I wanted to showcase the **Child Pages** underneath any **Parent Pages** without having to manually do so.

I didn't find any easy solutions to using Wordpress functions like `wp_list_pages` because for some reason it would spit out the query in `<li>` elements. While it may have been fine in theory, it wasn't the exact type of control I wanted where I was forced to style list elements.

Through some research of the WP documentation I wrote a special query like so:

```php
    <?php
    $child_links = array(
	    'post_type' => 'page',
	    'posts_per_page' => -1,
	    'post_parent' => $post->ID,
	    'order' => 'ASC',
	    'orderby' => 'menu_order');
	$parent = new  WP_Query( $child_links );
    ?>
```

And then spitting it out into the template like this:

```php
    <?php if ( $parent->have_posts() ) : ?>

		<?php  while ( $parent->have_posts() ) : $parent->the_post(); ?>
		<a  href="<?php  the_permalink(); ?>"  title="<?php  the_title(); ?>">
			<?php  the_title(); ?>
		</a>

	<?php
	endwhile;
	endif;
	wp_reset_postdata(); ?>
```

This would have been standard way of accomplishing this via WordPress functions.

But to make my life harder (and be more demanding of new tech), I decided I wanted to pull those Child Pages from the Wordpress API, into a custom Vue Dropdown Component for a more modern implementation.

Now, this may not be the smartest way to get this done, but I did want to start converting these elements into reusable Vue components. Not to mention there was a little bit of a time constraint, so I focused on building quickly and iterating later.

Before moving on, let's go ahead and create a couple test pages, and set the parent page of those child pages to the desired page. In this case, I named the parent page **Parent Page** and the Child Pages **Reviews** and **Resources**

To set the parent page, in your editor look along the right side for the Page Attributes setting. There you'll be able to select which page as the parent.

### Wordpress Rest API

So a neat little feature you can do with most Wordpress websites is get a JSON output of any available REST endpoints. You can do this by tacking on `/wp-json` to the end of the URL. I recommend using a browser extension like **JSON Formatter** that you can find on the Chrome Extensions Marketplace.

After digging through the file, you'll find that you're looking for the endpoint that displays the data for pages. You can see that at `wp/v2/pages`. We're only looking for a GET request, so based off of the [Wordpress Documentation](https://developer.wordpress.org/rest-api/reference/pages/) you can query a request from specific scheme like date, slug, type, author and so on.

What we are looking for is where any pages that have attribute **parent** equal to a specific page ID.

In my specific case, the parent page I'm looking at has the ID 217. Any pages that contain that ID I want to query.

To find this page ID, you'll usually find it appended to the URL while you're editing in the dashboard. For example: `/post.php?post=217&action=edit`

Using [Postman](https://www.getpostman.com/), I run `GET wp/v2/pages?parent=217`

In my case, I find that 2 entries (Reviews and Resources page IDs) pop up with the Parent ID equal the ID 217. Success!

### Using Axios

First let's install **axios** to make requests to the REST api.

```
    npm install axios --save-dev
```

You'll want to make sure you import this into your Vue component.

```js
// Import Vue JS
import Vue from 'vue'
import axios from 'axios'

new Vue({
  el: '#app',
  template: '<App/>',
  components: { App },
})
```

Now I've actually gone an implemented Single File Components into my workflow, so the following code may look a little different, but I feel it separates the code in a readable way.

We need to use axios to request from the endpoint.

```js
    data() {
	    return {
		    pages: []
	    }
    },
    mounted() {
	    axios.get(`/wp-json/wp/v2/pages?parent=217)
	    .then(response  => {
	    this.pages  =  response.data})
	    .catch(error  =>  console.log("Something went wrong"));
	 },
```

Here we set a variable pages, to receive the data from the Axios request. We also add a catch line, to give us a console log notification if the data does not process correctly.

I hardcoded the ID 217 mostly because I wanted to see if this would pull the data correctly.

### Filtering a JSON Response

Now for the purpose of the dropdown component, all I really need are two pieces of data

- Title
- Link

There is a third component you could work on, where Wordpress has a feature where you can set a page to **Password Protected** for only specific viewers to see. You wouldn't really want to showcase those pages in the dropdown, so the attribute would be

- content -> protected: false (where the filter won't include any password protected pages)

We won't write any code on that, but consider it a way to test more edge cases.

Now let's test this in the template:

```js
    <template>
	<a v-for='item in pages' :key="item.id" :href="item.link">
		{{ item.title.rendered }}
	</a>
    </template>
```

Success! What we did was loop over the pages array, setting the key to the ID, and iterating over the option element until there are no more items left.

Why `{{ item.title.rendered }}`?

For reasons above my own knowledge, Wordpress outputs the title in JSON like this `{ 'title': 'rendered': 'Title of Page' }` so we can select the piece of data we need by adding the rendered attribute.

Let's build the Vue component Dropdown, and make some changes to get the data.

### Building the Vue Component

Here's the code for Dropdown.vue with a few touches. I naturally use tailwind to build, but for the purposes of this article I broke it down into simple css.

```js
    //Dropdown.vue
    <template>
    <div class="dropdown-wrapper">
      <button @click="open = !open" type="button" class="dropdown-button">
        Navigate To     <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
        <path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
      </svg>
      </button>

      <div v-show="open" class="dropdown-menu">
            <slot></slot>
            <a v-for='item in pages' :key="item.id" :href="item.link">
              {{ item.title.rendered }}
            </a>
      </div>
    </div>
    </template>
    <script>
    import axios from 'axios';
    export default {
      name: "Dropdown",
      props: {
        page: {
          required: true
        }
      },
      data() {
        return {
          open: false,
          parentID: this.page,
          pages: []
        };
      },
      mounted() {
        console.log('The page id is ' + this.parentID);
        axios.get(`/wp-json/wp/v2/pages?parent=${this.parentID}`)
        .then(response => {
          this.pages = response.data
          console.log(this.pages)
        })
        .catch(error => console.log("Something went wrong."));
      },
    };
	</script>
```

```css
    <style scoped>
    .dropdown-wrapper {
      position: relative;
      margin: 0 auto;
    }

    .dropdown-button {
      display: flex;
      align-items: center;
      border: 2px solid #000;
      border-radius: .25rem;
      padding: 2rem .5rem;
      margin-bottom: .5rem;
    }

    .dropdown-button svg {
      display: block;
      vertical-align: middle;
      width: 1rem;
      height: 1rem;
      fill: currentColor;
    }

    .dropdown-menu {
      margin-top: 1px;
      border-radius: .25rem;
      background-color: #fff;
      box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
      width: auto;
      position: absolute;
      z-index: 10;
      overflow: hidden;
    }

    .dropdown-menu a {
	    display: block;
	    text-decoration: none;
	    padding: 1rem .75rem;
	    border-bottom-width: 1px;
	    white-space: nowrap;
    }

        </style>
```

In my main.js file, I make sure to require the component to use globally:

```js
Vue.component('dropdown', require('./vue/components/Dropdown.vue').default)
```

![background](/blog/vue-dropdown-closed.png)

### The Template

So I implemented a couple things into the component above:

In the template, you can see the component has a Button with text and an SVG and a Div (dropdown-menu) wrapped in (dropdown-wrapper). The button acts a trigger to set the data variable **open** to **true**. The menu itself will only show if true.

Inside of the dropdown menu are a few elements. A slot component (to insert hard links) and a v-for loop to iterate over the child data pulled from the parent.

For each iteration of the loop, we print `{{ item.title.rendered }}` which will display the title of the page being linked.

### Inside of Script

You can see that I've implemented props to store the Page ID. This takes the output of the Page ID and stores it in the Vue variable **parentID**.

In the mounted function, you'll notice we use **parentID** and pass it into the axios call to the REST API.

```js
axios.get(`/wp-json/wp/v2/pages?parent=${this.parentID}`)
```

We'll take this response and store it in the Vue data variable **pages** which gets iterated over and displayed in the template.

Simple enough!

### Passing Page ID as a Prop

So since we made the component global in the main.js file, you can use the element in your PHP templates.

To grab the page ID, in your template add this code:

```php
    <?php $page_id = get_the_ID(); ?>
```

Then you can go ahead and add your dropdown component, passing in the page ID to the prop.

```html
<dropdownmenu page_id="<?php" echo $page_id ?>
  >
  <a href="/about-us">About Us</a>
  <a href="/pricing">Pricing</a>
  <a href="/before-and-after">Before and After Gallery</a>
</dropdownmenu>
```

Remember the **slot** element we put in our Vue template?

Well we can add more links or any other element we want and it will appear above the child pages. Nifty huh?

### Wrapping Up

While trying to implement Vue into a custom theme, I realized there were several workarounds to getting something as simple as a dropdown to work correctly. That being said, I feel it's worth the work because I have much more control over the dropdown and its elements.

Taking it a step further, I might build upon this by adding a way to handle tapping/clicking outside of the dropdown component to close it. You could even look into adding animations or transitions.

Thanks for reading!
