<template>
  <div id="wrap">
    <!-- 视频块 -->
    <div class="video-box">
      <LivePlayer />
    </div>
    <!-- 时间轴 -->
    <div>
      <TimeBar />
    </div>
  </div>
</template>

<script>
import LivePlayer from "./components/LivePlayerDemo";
import TimeBar from "./components/TimeBar";
export default {
  name: "App",
  components: {
    LivePlayer,
    TimeBar
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
    position: absolute;
    width: 100%;
    height: 80%;
  }
}
</style>
