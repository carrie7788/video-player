<template>
  <!-- 刻度 -->
  <div class="scale-axis" ref="scaleAxis" id="maxBoxId">
    <!-- 左切按钮 -->
    <div class="toggle-btn">
      <img src="../assets/leftCut.png" alt="" />
    </div>
    <!-- 时间轴 -->
    <div class="center-box" ref="timelineBox">
      <div
        class="inner-box"
        id="timeline"
        ref="timeline"
        :style="{ width: '100%', left: '100%' }"
      >
        <!-- <ul>
          <li
            v-for="(item, index) in liNum"
            :key="index"
            :style="{ width: liWidth + 'px' }"
          >
            <div v-if="i === 0" class="mark-time">
              <span>{{ calcTime(index) }}</span>
            </div>
            <div v-if="i === 0" class="split-line">
              <span v-for="j in 10" :key="j" :class="{ first: j === 1 }"></span>
            </div>
            <div class="time-bar" :id="'timeBar' + i + '_' + index"></div>
          </li>
        </ul> -->
      </div>
    </div>
    <!-- 右切按钮 -->
    <div class="toggle-btn right-cut">
      <img src="../assets/rightCut.png" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      wndStyle: 1,
      liNum: 6
    };
  }
};
</script>

<style lang="less" scoped>
.scale-axis {
  height: 1rem;
  display: flex;
  align-items: center;
  // padding: 0 0.2rem;
  .toggle-btn {
    width: 0.2rem;
    cursor: pointer;
    &.right-cut {
      text-align: right;
    }
  }
  .center-box {
    position: relative;
    flex: 1;
    height: 100%;
    .inner-box {
      position: absolute;
      top: 0;
      left: 0;
      // > ul {
      //   .after-clear();
      //   > li {
      //     float: left;
      //     margin-top: -1px;

      //     .mark-time {
      //       box-sizing: border-box;
      //       background: #111418;
      //       border: 1px solid #090b0c;
      //       height: 20px;
      //       > span {
      //         color: #929495;
      //         font-size: 0.08rem;

      //         &:nth-child(1) {
      //           margin-left: -0.17rem;
      //         }
      //         &:nth-child(2) {
      //           float: right;
      //           margin-right: -0.17rem;
      //         }
      //       }
      //     }
      //     .split-line {
      //       width: 100%;
      //       height: 4px;
      //       span {
      //         float: left;
      //         width: 10%;
      //         height: 4px;
      //         border-left: 1px solid #929495;
      //         &.first {
      //           height: 0.07rem;
      //           margin-top: -0.03rem;
      //           margin-left: -0.01rem;
      //         }
      //       }
      //     }
      //     .time-bar {
      //       position: relative;
      //       height: 10px;
      //       background: #382b33;
      //       border-right: 1px solid #030405;
      //     }
      //   }
      // }
      .time-pointer {
        position: absolute;
        top: 0;
        left: 0;
        z-index: 3;
        .move-time {
          width: 60px;
          position: absolute;
          top: 0;
          left: -30px;
          color: #fff;
          font-size: 0.12rem;
          text-align: center;
        }
        .pointer-head {
          width: 10px;
          height: 4px;
          cursor: pointer;
          background-color: rgba(217, 68, 1, 0.8);
        }
        .pointer-line {
          width: 2px;
          position: absolute;
          top: 0;
          left: 4px;
          cursor: pointer;
          background-color: rgba(217, 68, 1, 0.8);
        }
      }
      .video-down {
        width: 100%;
        height: 20px;
        position: absolute;
        top: 0;
        left: 0;
        box-sizing: border-box;
        z-index: 2;

        ul,
        li {
          list-style: none;
          display: block;
          margin: 0;
          padding: 0;
        }
        .drag-box {
          width: 100%;
          height: 100%;
          overflow: hidden;
          .left-box {
            height: 100%;
            float: left;
          }
          .resize {
            width: 5px;
            height: 100%;
            cursor: w-resize;
            float: left;
            background-color: red;
            // background-color: hsl(210, 100%, 63%);
          }
          .right-box {
            height: 100%;
            float: left;
          }
          .mid-box {
            float: left;
            height: 100%;
            box-sizing: border-box;
            border-left: 1px solid #fff;
            border-right: 1px solid #fff;
          }
          .resize2 {
            width: 5px;
            height: 100%;
            cursor: w-resize;
            float: left;
            background-color: red;
            // background-color: #409eff;
          }
        }
      }
    }
    // 时间轴
    .hover-time {
      width: 60px;
      position: absolute;
      top: 0;
      left: 0;
      // padding: 5px;
      z-index: 3;
      border: 1px solid #646464;
      background: #ffffe1;
      font-size: 12px;
      color: #000033;
      text-align: center;
      letter-spacing: 0.5px;
    }
  }

  .lineSlide {
    position: absolute;
    left: 10px;
    width: 4px;
    height: 50px;
    top: 24px;
    background: red;
    z-index: 2000;
    cursor: pointer;
  }
  .lineArraw {
    position: absolute;
    top: -0.4rem;
    left: -0.5rem;
    width: 1rem;
    height: 1px;
    color: white;
    text-align: center;
  }
  .drag-class {
    background: rgba(255, 255, 255, 0);
    position: absolute;
    z-index: 1000;
    cursor: pointer;
    .drag-content {
      position: relative;
      height: 100%;
      .content-text {
        border: 1px dashed #ffffff;
        font-size: 0.16rem;
        color: #ffffff;
        position: relative;
        height: 100%;
        .drag-icon {
          position: absolute;
          right: 10px;
          top: 5px;
          float: left;
          // margin-right: 10px;
          .down-dragger {
            cursor: move;
            font-size: 30px;
            color: #dbdce0;
            color: #ffffff;
          }
        }
      }
    }
    .startTime {
      position: absolute;
      left: -15px;
      top: -35px;
      color: #fff;
    }
    .endTime {
      position: absolute;
      right: -25px;
      top: -35px;
      color: #fff;
    }
  }
}
</style>
