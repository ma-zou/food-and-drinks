<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Drinks</nuxt-link>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <posts post-type="drinks" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("drinks").fetch();
    } catch (e) {
      error({ message: "Projects not found" });
    }
    return { posts };
  },
}
</script>
