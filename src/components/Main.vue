<template>
  <div class="ma-3">
    <v-card class="border mb-5">
      <v-card-title>제목</v-card-title>
      <v-card-text>
        <v-text-field label="애니 제목" v-model="aniName" :rules="references.aniNameRules" required></v-text-field>
      </v-card-text>
      <v-card-text>
        <div>
          <p class="text-h6 pb-2">설정</p>
          <v-select
            label="화질"
            v-model="resolution"
            :items="references.resolutions"
            item-title="text"
            item-value="res"
          ></v-select>
          <v-checkbox label="통합본 안 받기" v-model="noAllEpisodes"></v-checkbox>
        </div>
      </v-card-text>
    </v-card>
    <v-card class="border">
      <v-card-title class="pb-0">결과</v-card-title>
      <v-card-text class="text-h5 pa-4">{{ aniNameRegex }}</v-card-text>
      <v-card-text class="pt-0">
        <v-btn
          :prepend-icon="copySuccess ? 'mdi-check' : 'mdi-content-copy'"
          variant="flat"
          :color="copySuccess ? 'success' : 'info'"
          @click="copy()"
        >
          복사
        </v-btn>
      </v-card-text>
    </v-card>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Main",

  data() {
    return {
      references: {
        aniNameRules: [(v: string) => !!v || "애니 제목을 입력하세요."],
        resolutions: [
          { res: "1280x720 x264 AAC(x2)?", text: "720p" },
          { res: "1920x1080 x265 AAC(x2)?", text: "1080p" },
          { res: "", text: "모두" },
        ],
      },

      aniName: "",
      aniNameRegex: "애니 제목을 입력하세요.",

      resolution: "1280x720 x264 AAC(x2)?",

      noAllEpisodes: false,

      copySuccess: false,
    };
  },

  methods: {
    updateRegex() {
      this.aniNameRegex =
        this.aniName !== ""
          ? `\\[Ohys-Raws\\] ${this.aniName.replace(/[.*+?^${}()|[\]\\]/g, "\\$&")}( - [0-9]*( END)?)${
              this.noAllEpisodes ? "" : "?"
            } \\(.* ${this.resolution}\\)`
          : "애니 제목을 입력하세요.";
    },
    copy() {
      if (this.aniNameRegex !== "애니 제목을 입력하세요.") {
        navigator.clipboard.writeText(this.aniNameRegex);
        this.copySuccess = true;
        setTimeout(() => {
          this.copySuccess = false;
        }, 2000);
      }
    },
  },

  watch: {
    aniName() {
      this.updateRegex();
    },
    resolution() {
      this.updateRegex();
    },
    noAllEpisodes() {
      this.updateRegex();
    },
  },
});
</script>

<style>
.v-input__details {
  display: none !important;
}
</style>
