<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <h1>This is my Cool PWA</h1>
      <button v-if="updateAvailable">Click to update</button>
      <p>This site is created by Wout</p>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    registration: null,
    updateAvailable: false,
  }),

  components: {
    
  },

  created() {
    document.addEventListener(
      'swupdatefound', this.updateTheApp, { once: true }
    );
  },

  methods: {
    updateTheApp(e) {
      this.registration = e.detail;
      this.updateAvailable = true;
    },
    // Actual update
    update(){
      this.updateAvailable = false;
      // Lazy evaluation
      if (this.registration || this.registration.waiting) {
        this.registration.waiting.postMessage({type:'SKIP_WAITING'});
      }
    },
  },
};
</script>
