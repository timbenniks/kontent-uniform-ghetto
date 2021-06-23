<template>
  <section class="component bg-white text-black rounded-xl p-3 m-2">
    <h1>{{ title }}</h1>
    <div v-html="description"></div>
  </section>
</template>
<script>
export default {
  name: 'RichText',
  props: {
    data: { type: Object, required: true },
    tracking: { type: Boolean, required: false, default: true },
  },

  computed: {
    description() {
      return this.data.description.value
        ? this.data.description.value
        : this.data.description
    },

    title() {
      return this.data.title.value ? this.data.title.value : this.data.title
    },
  },

  mounted() {
    if (this.tracking) {
      const intentTag = JSON.parse(this.data.intent_tags.value)

      this.$uniformOptimize.trackBehavior(intentTag)
    }
  },
}
</script>
