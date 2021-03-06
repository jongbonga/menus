<template>
  <b-container fluid class="h-100" :class="place.background">
    <b-row class="h-100 justify-content-center align-content-center">
      <b-col cols="auto" sm="8" md="6">
        <b-card
          :title="`Explore ${place.name} using the mobile App`"
          title-tag="h2"
          sub-title="ACCESS MENUS & EXCLUSIVE SPECIALS!"
          footer-bg-variant="white"
          footer-border-variant="white"
          footer-class="text-center"
          class="shadow-lg border-0 overflow-hidden  text-center"
          style="border-radius:10px"
          :img-src="place.image"
        >
          <template #footer>
            <div class="d-none d-sm-block">
              <div class="d-flex justify-content-around">
                <b-button
                  v-for="button in place.buttons"
                  :key="button.text"
                  :variant="button.color"
                  @click="action(button.action)"
                >
                  {{ button.text }} <b-icon :icon="button.icon"></b-icon>
                </b-button>
              </div>
            </div>

            <b-button-group class="d-block d-sm-none">
              <b-button
                v-for="button in place.buttons"
                :key="button.text"
                :variant="button.color"
                @click="action(button.action)"
              >
                {{ button.text }} <b-icon :icon="button.icon"></b-icon>
              </b-button>
            </b-button-group>
          </template>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import palceData from "@/data/data.json";
export default {
  name: "Home",
  palceData: palceData,
  computed: {
    place() {
      const place = this.$options.palceData.filter(
        ({ name }) =>
          name.toLowerCase() === this.$route.params.name.toLowerCase()
      );
      return place[0];
    }
  },
  methods: {
    action(action) {
      console.log(action);
      action === "downloadApp" ? this.downloadApp() : this.openMenu();
    },
    openMenu() {
      const url = "https://theathletic.co.za/AthleticMenuSeptember.pdf";
      window.open(url, "_blank");
    },
    downloadApp() {
      const ios =
        [
          "iPad Simulator",
          "iPhone Simulator",
          "iPod Simulator",
          "iPad",
          "iPhone",
          "iPod"
        ].includes(navigator.platform) || navigator.userAgent.includes("Mac");

      const store = ios ? this.place.store.ios : this.place.store.android;
      window.open(store);
    }
  }
};
</script>
