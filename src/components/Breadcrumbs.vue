<template>
  <div class="py-1 px-2">
    <client-only>
      <v-breadcrumbs v-if="breadcrumbsItems.length > 0" class="pa-0" :items="breadcrumbsItems">
        <template #divider>
          <v-icon color="grey">
            mdi-menu-right
          </v-icon>
        </template>
        <template #item="{ item }">
          <v-breadcrumbs-item :disabled="!item.to">
            <nuxt-link v-if="item.to" class="grey--text" :to="localePath(item.to)" v-text="item.text" />
            <span v-else class="grey--text" v-text="item.text" />
          </v-breadcrumbs-item>
        </template>
      </v-breadcrumbs>
    </client-only>
  </div>
</template>

<script>
export default {
  computed: {
    breadcrumbsItems () {
      return this.$store.state.breadcrumbs && this.$store.state.breadcrumbs.breadcrumbsItems ? this.$store.state.breadcrumbs.breadcrumbsItems : []
    }
  }
}
</script>
