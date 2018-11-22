<template>
  <div>
    <v-btn
    class="media-button"
    @click="didClick">
      <v-icon class="play-icon">{{playing ? 'stop' : 'play_arrow'}}</v-icon>
      <h3>{{title}}</h3>
    </v-btn>
  </div>
</template>

<script>
  import VueHowler from 'vue-howler'

  export default {
    mixins: [VueHowler],
    props: {
      title: String,
    },
    methods: {
      didClick() {
        if (this.playing) {
          this.stop()
        } else {
          this.play()
        }
        this.$emit('did-click')
      }
    }
  }
</script>

<style scoped>
.play-icon {
  padding-right: 10px;
}
h3 {}
</style>
