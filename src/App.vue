<script setup>
  import { computed } from 'vue'
  import jsonData from '@/assets/data.json';

  const filterBoorus = (category) => computed(() => 
    jsonData.filter(website => website.category === category)
  );

  const art_boorus = filterBoorus('general');
  const anime_boorus = filterBoorus('anime');
  const furry_boorus = filterBoorus('furry');
  const interest_boorus = filterBoorus('interest');
  const real_boorus = filterBoorus('real');

  const urlParams = new URLSearchParams(window.location.search);
  const tag = urlParams.get('tag');

  function format_search_url(site) {
    const protocol = site.protocol || 'https';
    const search = site.search.replace('$1', tag);
    return `${protocol}://${site.domain}/${search}`;
  }

  function format_wiki_url(site) {
    const protocol = site.protocol || 'https';
    if (!site.wiki) { return null; }
    const wiki = site.wiki.replace('$1', tag);
    return `${protocol}://${site.domain}/${wiki}`;
  }
</script>

<template>
  <h2>{{ tag }}</h2>
  <div class="categories">
    <div class="category">
      <h3>Anime / Manga</h3>
      <ul>
        <li v-for="website in anime_boorus">
          <img :src="`/icons/${website.domain}.png`" :alt="website['name']" class="icon">
          <a :href="format_search_url(website)">#{{ tag }} on <strong>{{ website["name"] }}</strong></a>
          <span v-if="format_wiki_url(website)">(<a :href="format_wiki_url(website)">wiki</a>)</span>
          <span v-if="website['nsfw']" class="nsfw">NSFW</span>
        </li>
      </ul>
    </div>
    <div class="category">
      <h3>Furry</h3>
      <ul>
        <li v-for="website in furry_boorus">
          <img :src="`/icons/${website.domain}.png`" :alt="website['name']" class="icon">
          <a :href="format_search_url(website)">#{{ tag }} on <strong>{{ website["name"] }}</strong></a>
          <span v-if="format_wiki_url(website)">(<a :href="format_wiki_url(website)">wiki</a>)</span>
          <span v-if="website['nsfw']" class="nsfw">NSFW</span>
        </li>
      </ul>
    </div>
    <div class="category">
      <h3>General Art</h3>
      <ul>
        <li v-for="website in art_boorus">
          <img :src="`/icons/${website.domain}.png`" :alt="website['name']" class="icon">
          <a :href="format_search_url(website)">#{{ tag }} on <strong>{{ website["name"] }}</strong></a>
          <span v-if="format_wiki_url(website)">(<a :href="format_wiki_url(website)">wiki</a>)</span>
          <span v-if="website['nsfw']" class="nsfw">NSFW</span>
        </li>
      </ul>
    </div>
    <div class="category">
      <h3>Specific Interests</h3>
      <ul>
        <li v-for="website in interest_boorus">
          <img :src="`/icons/${website.domain}.png`" :alt="website['name']" class="icon">
          <a :href="format_search_url(website)">#{{ tag }} on <strong>{{ website["name"] }}</strong></a>
          <span v-if="format_wiki_url(website)">(<a :href="format_wiki_url(website)">wiki</a>)</span>
          <span v-if="website['nsfw']" class="nsfw">NSFW</span>
        </li>
      </ul>
    </div>
    <div class="category">
      <h3>Real</h3>
      <ul>
        <li v-for="website in real_boorus">
          <img :src="`/icons/${website.domain}.png`" :alt="website['name']" class="icon">
          <a :href="format_search_url(website)">#{{ tag }} on <strong>{{ website["name"] }}</strong></a>
          <span v-if="format_wiki_url(website)">(<a :href="format_wiki_url(website)">wiki</a>)</span>
          <span v-if="website['nsfw']" class="nsfw">NSFW</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
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
