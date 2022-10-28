<template>
  <div id="wrap">
    <!-- 视频块 -->
    <div class="video-box">
      <LivePlayer />
    </div>
  </div>
</template>

<script>
import LivePlayer from "./components/LivePlayerDemo";
export default {
  name: "App",
  components: {
    LivePlayer
  }
};
</script>

<style lang="less" scoped>
#wrap {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  box-sizing: border-box;
  .video-box {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    box-sizing: border-box;
  }
}
</style>
