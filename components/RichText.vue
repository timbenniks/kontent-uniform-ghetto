<template>
  <section class="component bg-black text-white rounded-xl p-3 m-8">
    <div class="content" v-html="data.rich_text.value"></div>
  </section>
</template>
<script>
export default {
  name: 'RichText',
  props: {
    data: { type: Object, required: true },
  },
}
</script>
