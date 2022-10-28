<template>
  <div id="videoWrap">
    <LivePlayer
      :videoUrl="videoUrl"
      fluent
      autoplay
      live
      :stretch="false"
      aspect="fullscreen"
    />
  </div>
</template>

<script>
import LivePlayer from "@liveqing/liveplayer"; // vue2

export default {
  data() {
    return {
      videoUrl: "http://vjs.zencdn.net/v/oceans.mp4"
    };
  },
  components: {
    LivePlayer
  },
  methods: {}
};
</script>
