<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Recipies</nuxt-link>
    <ul class="selectionNavi big">
      <li>
        <nuxt-link class="btn overlay" to="/drinks">
          <span class="text">Drinks</span>
          <video src="img/drinks.mp4" ref="drinks" loop muted autoplay></video>
          <span class="counter">{{ drinks }} Drinks</span>
        </nuxt-link>
      </li>
      <li>
        <nuxt-link class="btn overlay" to="/food">
          <span class="text">Food</span>
          <video src="img/food.mp4" loop muted autoplay></video>
          <span class="counter">{{ food }} Recipies</span>
        </nuxt-link>
      </li>
    </ul>
  </main>
</template>

<script>
export default {
  data() {
    return {
      drinks: 0,
      food: 0
    }
  },
  async asyncData({ $content, error }) {
    let drinks;
    let food;
    try {
      drinks = await $content("drinks").fetch();
      food = await $content("food").fetch();
    } catch (e) {
      error({ message: "Projects not found" });
    }
    return { drinks: drinks.length, food: food.length };
  },
  mounted() {
    this.$refs.drinks.playbackRate = 0.3;
  }
}
</script>
