<template>
  <div id="app">
    <v-toolbar
      class="toolbar"
      :fixed="true"
      :flat="true"
      :extended="true"
      extension-height="40px"
      color="#673ab7">
      <audio-player
        :sources="test"
        v-on:did-click="didPlayTest=true"
        title="Test" />
      <audio-player
        :sources="track1"
        v-on:did-click="didPlay1=true"
        title="Track 1" />
      <audio-player
        :sources="track2"
        v-on:did-click="didPlay2=true"
        title="Track 2" />
      <h2
        class="rightAlign">
        Code:
        <v-chip class="chip">
          <v-avatar>
            <v-icon>check_circle</v-icon>
          </v-avatar>
          {{completionCode}}
        </v-chip>
      </h2>
      <br>
      <p slot="extension">
        Please don't click these buttons until you are instructed to do so in the survey below.
      </p>
    </v-toolbar>
    <div class="form-container">
      <iframe src="https://docs.google.com/forms/d/e/1FAIpQLSe61Omxa5Vr_brKt0uVJ6G8wKqiVTtBTn7Mf0Kgw4MhEvVIRA/viewform" width="100%" height="100%" frameborder="0" marginheight="0" marginwidth="0">Loading...</iframe>
    </div>
  </div>
</template>

<script>
import AudioPlayer from './AudioPlayer.vue'

export default {
  name: 'app',
  components: {
    AudioPlayer
  },
  data() {
    return {
      didPlay1: false,
      didPlay2: false,
      didPlayTest: false,

      test: [
        require("./assets/test.mp3"),
        require("./assets/test.wav")
      ],
      edm: [
        require('./assets/track1.mp3')
      ],
      classical: [
        require('./assets/track2.mp3')
      ],

      variant: null
    }
  },
  computed: {
    track1: function() {
      return this.variant == 0 ? this.edm : this.classical
    },
    track2: function() {
      return this.variant == 0 ? this.classical : this.edm
    },
    completionCode: function() {
      return this.variant == 0 ? "NQX" : "RST"
    }
  },
  mounted() {
    this.variant = Math.floor(Math.random() * 2)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  height: 100vh;
  width: 100vw;
}
.rightAlign {
  position: absolute;
  right: 20px;
}
.form-container {
  /* padding-top: 104px; */
  height: 100%;
}
.toolbar {
  padding-top: 15px;
}
.chip {
  padding-right: 20px;
}
p, h2 {
  color: white
}
p {
  padding-left: 8px;
}
</style>
