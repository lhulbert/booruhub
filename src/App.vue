<script setup>
  import { computed } from 'vue'
  import BooruListing from '@/BooruListing.vue'
  import jsonData from '@/assets/data.json';

  const filterBoorus = (category) => computed(() => 
    jsonData.filter(website => website.category === category)
  );

  const anime_boorus = filterBoorus('anime');
  const furry_boorus = filterBoorus('furry');
  const interest_boorus = filterBoorus('interest');

  const urlParams = new URLSearchParams(window.location.search);
  const tag = urlParams.get('tag');
</script>

<template>
  <h2>{{ tag }}</h2>
  <div class="categories">
    <div class="category">
      <h3>Anime / Manga / General Art</h3>
      <ul>
        <li v-for="website in anime_boorus">
          <BooruListing :website="website" :tag="tag"></BooruListing>
        </li>
      </ul>
    </div>
    <div class="category">
      <h3>Specific Interests / Real</h3>
      <ul>
        <li v-for="website in interest_boorus">
          <BooruListing :website="website" :tag="tag"></BooruListing>
        </li>
      </ul>
    </div>
    <div class="category">
      <h3>Furry / MLP / Fetish</h3>
      <ul>
        <li v-for="website in furry_boorus">
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
    margin: 0;
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
