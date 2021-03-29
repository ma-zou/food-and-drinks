<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Drinks</nuxt-link>
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
      console.log($content("drinks").fetch());
      post = await $content("drinks", params.drinks).fetch();

      console.log('POST: ', post);
    } catch (e) {
      error({ message: "Project not found" });
    }
    return { post };
  },
}
</script>
