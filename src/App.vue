<script setup>
  import { computed, ref } from 'vue';
  import BooruListing from '@/BooruListing.vue';
  import jsonData from '@/assets/data.json';

  const show_nsfw = ref(false);
  
  const categories = [
    { title: "Anime / Manga / General Art", "category": "anime" },
    { title: "Specific Interests / Real", "category": "interest" },
    { title: "Furry / MLP / Fetish", "category": "furry" },
  ];

  const filteredCategories = computed(() =>
  categories.map((category) => ({
    title: category.title,
    filteredBoorus: jsonData.filter(
      (website) =>
        website.category === category.category &&
        (!website.nsfw || show_nsfw.value)
    ),
  }))
);

  const urlParams = new URLSearchParams(window.location.search);
  const tag = urlParams.get('tag');
</script>

<template>
  <h2>{{ tag }}</h2>
  <button v-if="!show_nsfw" @click="show_nsfw = true">Show NSFW</button>
  <button v-if="show_nsfw" @click="show_nsfw = false">Hide NSFW</button>
  <div class="categories">
    <div class="category" v-for="category in filteredCategories" :key="category.title">
      <h3>{{ category.title }}</h3>
      <ul>
        <li v-for="website in category.filteredBoorus" :key="website.domain">
          <BooruListing :website="website" :tag="tag"></BooruListing>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
  body {
    font-family: Arial, sans-serif;
    margin: 20px;
  }

  h2 {
    text-align: center;
  }

  button {
    display: block;
    margin: 0 auto;
  }

  .categories {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
  }

  .category {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .category h3 {
    font-size: 1.2em;
    text-align: center;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  li {
    display: flex;
    align-items: center;
    gap: 10px;
    border-bottom: solid 1px grey;
  }

  .icon {
    width: 24px;
    height: 24px;
  }

  a {
    text-decoration: none;
    color: #000;
  }

  a:hover {
    text-decoration: underline;
  }

  .nsfw {
    background-color: #dd4444;
    color: white;
    padding: 2px 4px;
    border-radius: 3px;
    font-size: 0.8em;
    margin-left: 5px;

  }
</style>
