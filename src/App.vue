<template>
  <v-app>
    <v-main>
      <Main />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Main from "./components/Main.vue";

export default defineComponent({
  name: "App",

  components: { Main },
});
</script>
