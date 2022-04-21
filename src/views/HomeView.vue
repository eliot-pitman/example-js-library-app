<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import * as Tone from "tone";

export default {
  data: function () {
    return {
      isActive: false,
    };
  },
  methods: {
    toggle: function () {
      this.isActive = !this.isActive;
      console.log(this.isActive);
    },
    noise: function () {
      this.isActive = !this.isActive;
      console.log(this.isActive);
      if (this.isActive === true) {
        // initialize the noise and start
        const noise = new Tone.Noise("pink").start();
        // make an autofilter to shape the noise
        const autoFilter = new Tone.AutoFilter({
          frequency: "8n",
          baseFrequency: 200,
          octaves: 8,
        })
          .toDestination()
          .start();
        // connect the noise
        noise.connect(autoFilter);
        // start the autofilter LFO
        autoFilter.start();
      }
    },
  },
  created: function () {},
};
</script>

<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <button @click="noise">Get some Noise!</button>
    <h1 v-show="isActive === true">GOTCHA!!</h1>
    <p v-show="isActive === true">(refresh the page)</p>
  </div>
</template>

<style>
h1 {
  font-size: 75px;
}
</style>
