<template>
  <div class="font-sans text-gray-900 min-h-screen flex flex-col max-w-screen-lg lg:max-w-full">
    <AppHeader />
    <main class="flex-auto overflow-hidden absolute inset-0 pt-16 flex">
      <Sidebar />
      <FlexContainer v-if="showFlexMarkup === false" />
      <FlexMarkup v-else />
    </main>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import AppHeader from './components/AppHeader.vue'
import Sidebar from './components/Sidebar.vue'
import FlexContainer from './components/FlexContainer.vue'
import FlexMarkup from './components/FlexMarkup.vue'

export default {
  name: 'FlexboxPlayground',
  components: {
    AppHeader,
    Sidebar,
    FlexContainer,
    FlexMarkup
  },
  computed: {
    ...mapState(['showFlexMarkup'])
  },
  mounted() {
    const { timeZone, locale } = Intl.DateTimeFormat().resolvedOptions()
    fetch('/api/pageview', {
      method: 'POST',
      body: JSON.stringify({ timeZone, locale }),
      headers: { 'Content-Type': 'application/json' }
    })
  },
}
</script>
