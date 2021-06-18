<template>
  <section class="component bg-white text-black rounded-xl p-3 m-2">
    <h1>{{ data.title }}</h1>
    <div v-html="data.description"></div>
  </section>
</template>
<script>
export default {
  name: 'RichText',
  props: {
    data: { type: Object, required: true },
    tracking: { type: Boolean, required: false, default: true },
  },

  mounted() {
    if (this.tracking) {
      this.$uniformOptimize.trackBehavior(this.data.intentTag)
    }
  },
}
</script>
