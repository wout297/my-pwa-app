<template>
  <v-app>
    <v-main>
      <h1>This is my Cool PWA</h1>
      <v-btn v-if="updateAvailable" @click="update">Click to update</v-btn>
      <p>This site is created by Wout Peirens @ VIVES</p>
      <p>new paragraphs</p>
      <p>This was a demo for mobile apps</p>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    registration: null,
    updateAvailable: false,
    isRefreshing: false
  }),

  components: {
    
  },

  created() {
    document.addEventListener(
      'swupdatefound', this.updateTheApp, { once: true }
    );

    navigator.serviceWorker.addEventListener(
      'controllerchange', () => {
        if (this.isRefreshing) return;
        this.isRefreshing = true;
        window.location.reload();
      }
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
