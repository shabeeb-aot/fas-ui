<template>
  <div v-if="items && items.length > 0" class="background-color">
    <v-container class="d-flex flex-row py-0">
      <v-btn
        icon
        @click="goBack"
        class="font-weight-bold"
        data-test="btn-back"
        x-large
        v-if="items.length > 1"
      >
        <v-icon class="white-color ">mdi-arrow-left-circle</v-icon>
      </v-btn>
      <v-divider v-if="items.length > 1" color="white" class="my-2 ml-2 mr-4" vertical/>
      <v-breadcrumbs :items="items" class="pa-0">
        <template v-slot:divider>
          <v-icon color="white">mdi-chevron-right</v-icon>
        </template>
        <template v-slot:item="{ item }">
          <v-breadcrumbs-item
            :to="item.to"
            :href="item.href"
            class="text-subtitle-2 crumb-item"
            :disabled="item.disabled"
            exact
          >
            <span class="my-2 text-color" :class="item.disabled ? '' : 'text-decoration-underline'"> {{ item.text }} </span>
          </v-breadcrumbs-item>
        </template>
      </v-breadcrumbs>
    </v-container>
  </div>
</template>

<script lang="ts">
import { useBreadCrumb } from '@/composables/common'
import { Component, Vue } from 'vue-property-decorator'

@Component({
  setup (_, context) {
    const { items, goBack } = useBreadCrumb(_, context)
    return {
      items,
      goBack
    }
  }
})
export default class BreadCrumb extends Vue {
}
</script>

<style lang="scss" scoped>
@import '$assets/scss/theme.scss';
  .background-color {
    background-color: $BCgoveBueText1;
  }
  .text-color {
    color: $BCgovBG;
  }
  .white-color {
    color: $BCgovInputBG !important;
  }
</style>
