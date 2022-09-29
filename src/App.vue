<template>
  <v-app>
    <v-main>
      <Main />
    </v-main>
    <v-footer>
      <v-card elevation="0" rounded="0" width="100%" class="text-center">
        <v-catd-text>
          <v-btn icon="mdi-github" variant="plain" @click="openGithub()"></v-btn>
        </v-catd-text>
        <br />
        <v-catd-text> {{ new Date().getFullYear() }} — <strong>Alanimdeo</strong> </v-catd-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Main from "./components/Main.vue";

export default defineComponent({
  name: "App",

  components: { Main },

  methods: {
    openGithub() {
      window.open("https://github.com/alanimdeo/ohys-regex-generator");
    },
  },
});
</script>
