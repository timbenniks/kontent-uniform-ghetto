<template>
  <div class="container">
    <component
      :is="mapComponentName(component.system.type)"
      v-for="component in pageComponents"
      :key="component.system.id"
      :data="component"
    />
  </div>
</template>

<script>
import toPascalCase from 'to-pascal-case'

export default {
  async asyncData({ route, $deliveryClient }) {
    const slug =
      route.path === '/' || route.path === '' ? 'home-page' : route.path

    const page = await $deliveryClient
      .items('page')
      .type('page')
      .depthParameter(3)
      .equalsFilter('elements.slug', slug)
      .toPromise()

    return { pageComponents: page.items[0].page_components.value }
  },

  watch: {
    '$route.query'() {
      this.reevaluateSignals()
    },
  },

  methods: {
    mapComponentName(name) {
      return toPascalCase(name)
    },
    reevaluateSignals() {
      if (!this.$uniformOptimizeContext.trackerInitializing) {
        this.$uniformOptimizeContext.tracker.reevaluateSignals()
      }
    },
  },
}
</script>
