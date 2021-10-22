<template>
  <v-app>
    <v-app-bar absolute app dark style="background: linear-gradient(0.25turn, #de7fff, #2fcfb6);">
      <v-btn icon to="/" class="mx-3">
        <v-avatar>
          <v-img src="/asset/logo.png" />
        </v-avatar>
      </v-btn>

      <h1>theBULL</h1>

      <v-spacer />

      <v-btn v-for="icon in socials" :key="icon.icon" icon class="mr-2 white--text" :href="icon.link" target="_blank">
        <v-icon size="24px">{{ icon.icon }}</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12" md="8">
            <v-card outlined>
              <BullComposer :images="currentImages" />
            </v-card>
          </v-col>

          <v-col cols="12" md="4">
            <v-select outlined v-model="selectedTraitType" :items="traitTypes" />
            <v-card outlined>
              <v-list v-if="selectedTraitType">
                <v-list-item-group v-model="selectedTraitIndex" color="primary">
                  <v-list-item
                    two-line
                    v-for="trait in traits.filter((c) => c.trait_type == selectedTraitType)"
                    :key="trait.name"
                  >
                    <v-list-item-content>
                      <v-list-item-title>{{ trait.value }}</v-list-item-title>
                      <v-list-item-subtitle>{{ trait.share }}</v-list-item-subtitle>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";

import traits from "@/docs/rarities.json";
import BullComposer from "@/components/BullComposer.vue";

export default Vue.extend({
  name: "App",
  components: { BullComposer },
  data: () => ({
    socials: [
      {
        icon: "fab fa-discord",
        alt: "Discord",
        link: "https://discord.gg/metacollective",
      },
      {
        icon: "fab fa-twitter",
        alt: "Twitter",
        link: "https://twitter.com/theBULL_NFT",
      },
    ],
    traits,
    selectedTraitType: traits.map((c) => c.trait_type).filter((v, i, a) => a.indexOf(v) === i)[0],
    selectedTraitIndex: 0,
  }),
  computed: {
    traitTypes(): string[] {
      return traits.map((c) => c.trait_type).filter((v, i, a) => a.indexOf(v) === i);
    },
    currentImages() {
      var ret = ["/asset/silhouette.jpg"];
      const selectedTrait = traits.filter((c) => c.trait_type == this.selectedTraitType)[this.selectedTraitIndex];
      if (selectedTrait) {
        ret.push(selectedTrait.path);
      }
      return ret;
    },
  },
});
</script>
