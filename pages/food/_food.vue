<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Food</nuxt-link>
    <section v-if="post">
      <article>
        <div class="content">
          <h1 class="">{{ post.title }}</h1>
          <p class="desc">{{ post.description }}</p>
          <h6>{{ post.category }}</h6>
          <nuxt-content class="ingredients" :document="post" />
          <p>{{ post.info }}</p>
        </div>
        <div v-if="post.cover" class="image">
          <img
            class="cover-image"
            :src="post.cover"
          >
        </div>
      </article>
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("food", params.food).fetch();
    } catch (e) {
      error({ message: "Blog post not found" });
    }
    return { post };
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    }
  }
}
</script>
