<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Food</nuxt-link>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <posts post-type="food" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("food").fetch();
    } catch (e) {
      error({ message: "Blog posts not found" });
    }
    return { posts };
  },
}
</script>
