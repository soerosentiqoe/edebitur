<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-cyan-8">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          eDebitur
        </q-toolbar-title>

        <div>Versi {{ versi }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
        :width="200"
        :breakpoint="400"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >

        </q-item-label>
        <PageMenu

        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import PageMenu from 'components/PageMenu.vue'

export default {
  name: 'MainLayout',
  components: { PageMenu },
  data () {
    return {
      leftDrawerOpen: false,
      versi: '14.0 beta'

    }
  }
}
</script>
