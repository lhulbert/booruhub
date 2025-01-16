<script setup>

defineProps({
    website: {
      type: Object,
      required: true
    },
    tag: {
      type: String,
      required: true
    },
  }
);

  function format_search_url(site, tag) {
    const protocol = site.protocol || 'https';
    const search = site.search.replace('$1', tag);
    return `${protocol}://${site.domain}/${search}`;
  }

  function format_wiki_url(site, tag) {
    const protocol = site.protocol || 'https';
    if (!site.wiki) { return null; }
    const wiki = site.wiki.replace('$1', tag);
    return `${protocol}://${site.domain}/${wiki}`;
  }

</script>

<template>
  <img :src="`./icons/${website.domain}.png`" :alt="website['name']" class="icon">
  <a :href="format_search_url(website, tag)">#{{ tag }} on <strong>{{ website["name"] }}</strong></a>
  <span v-if="format_wiki_url(website, tag)">(<a :href="format_wiki_url(website)">wiki</a>)</span>
  <span v-if="website['nsfw']" class="nsfw">NSFW</span>
</template>

<style scoped>

</style>