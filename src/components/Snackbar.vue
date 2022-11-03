<template>
  <v-snackbar v-model="show" :color="color">
    <slot name="default">
      <div class="d-flex align-center">
        <v-icon v-if="icon" size="x-large" start>
          {{ icon }}
        </v-icon>

        <div>
          <h2 v-if="title" class="font-weight-light">
            {{ title }}
          </h2>
          <p v-if="content" class="mt-1 mb-0">
            {{ content }}
          </p>
        </div>
      </div>
    </slot>
    <template #actions>
      <slot name="actions">
        <v-btn variant="plain" @click="show = false">
          {{ $t("CLOSE") }}
        </v-btn>
      </slot>
    </template>
  </v-snackbar>
</template>

<script setup lang="ts">
import { ref } from "vue";
import type { Ref } from "vue";

const show: Ref<boolean> = ref(false);
const title: Ref<string> = ref("");
const content: Ref<string> = ref("");
const color: Ref<string> = ref("");
const icon: Ref<string> = ref("");

export default {
  data() {
    return {
      icons: {
        success: "fas fa-check",
        info: "fas fa-info-circle",
        warning: "fas fa-exclamation-triangle",
        error: "fas fa-times-circle",
      },
      show: false,
      title: "",
      content: "",
      color: "",
      icon: "",
    };
  },

  created() {
    this.$store.subscribe((mutation, state) => {
      if (mutation.type === "snackbar/showMessage") {
        this.title = state.snackbar.title;
        this.content = state.snackbar.content;
        this.color = state.snackbar.color;
        this.icon = state.snackbar.icon
          ? state.snackbar.icon
          : this.icons[state.snackbar.color];
        this.show = true;
      }
    });
  },
};
</script>
