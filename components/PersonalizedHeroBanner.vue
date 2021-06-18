<template>
  <section class="component bg-black text-white rounded-xl p-3 m-8">
    <personalize :variations="variants">
      <template #default="{ variations, personalized }">
        <hero-banner :tracking="false" :data="variations[0]" />
        <p>
          <strong>Personalized: {{ personalized }}</strong>
        </p>
      </template>
    </personalize>
  </section>
</template>
<script>
import { Personalize } from '@uniformdev/optimize-tracker-vue'

export default {
  name: 'PersonalizedHeroBanner',
  components: {
    Personalize,
  },
  props: {
    data: { type: Object, required: true },
  },
  computed: {
    variants() {
      return this.data.unfrmoptp13nlist.value.map((variant) => {
        const intentTags = JSON.parse(variant.intent_tags.value) || {
          intents: {},
        }
        return {
          title: variant.title.value,
          description: variant.description.value,
          intentTag: { ...intentTags },
        }
      })
    },
  },
}
</script>
