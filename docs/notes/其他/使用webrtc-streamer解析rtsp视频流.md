# 一、webrtc-streamer

- WebRTC (Web Real-Time Communications) 是一项实时通讯技术，它允许网络应用或者站点，在不借助中间媒介的情况下，建立浏览器之间点对点（Peer-to-Peer）的连接，实现视频流和（或）音频流或者其他任意数据的传输。WebRTC 包含的这些标准使用户在无需安装任何插件或者第三方的软件的情况下，创建点对点（Peer-to-Peer）的数据分享和电话会议成为可能。
  ```bash
  简单的说：WebRTC 是一种 HTML5规范，他无需在浏览器中安装任何插件可以在网页内进行实时通信工作的开源技术，它直接在浏览器和设备之间添加实时媒体通信。
  ```
- rtsp（Real Time Streaming Protocol，RTSP）是实时视频网络传输主流的实现方式，是一种网络流媒体协议。低延时高清晰度的 RTSP 视频流传输是网络直播、在线会议系统等行业的核心技术。

- webrtc-streamer 是一个使用简单机制通过 WebRTC 流式传输视频捕获设备和 RTSP 源的项目,它内置了一个小型的 HTTP server 来对 WebRTC 需要的相关接口提供支持。

# 二、使用方法

## 1、下载 webrtc-streamer

```
https://github.com/mpromonet/webrtc-streamer/releases
```

## 2、运行

```
双击解压后的.exe文件运行，默认抛出本机8000端口（172.0.0.1:8000）
```

- 由于 webrtc 的核心库还不支持 H265 的视频编码，所以要配置设备视频编码方式为 H264
- 命令：-o ，默认情况 video 会进行编码、解码，占用资源，可能导致 cpu 拉满，使用-o 将取消编码解码
- 自定义端口：创建.bat 文件，并双击执行，文件内容如下：
  ```bash
  @echo off
  start "" ".\webrtc-streamer.exe"  -H 0.0.0.0:9998 -o
  exit
  ```
- 运行成功后，可在浏览器中查询所有 api
  ```js
  //192.168.3.33:9998/api/help
  http: [
    "/api/addIceCandidate",
    "/api/call",
    "/api/createOffer",
    "/api/getAudioDeviceList",
    "/api/getAudioPlayoutList",
    "/api/getIceCandidate",
    "/api/getIceServers",
    "/api/getMediaList",
    "/api/getPeerConnectionList", // 判断当前的webrtc-streamer正在连接的通道
    "/api/getStreamList",
    "/api/getVideoDeviceList",
    "/api/hangup",
    "/api/help",
    "/api/log",
    "/api/setAnswer",
    "/api/version",
    "/api/whep",
  ];
  ```

## 3、引用开发包

- 将下载包 html 文件夹下`webrtcstreamer.js`文件和 html/libs 文件夹下`adapter.min.js`文件复制到 VUE 项目 public 目录下 、在 index.html 文件里引入这两个 js 文件
  ```html
  <head>
    <!-- rtsp -->
    <script src="/data/webrtcstreamer.js" charset="utf-8"></script>
    <script src="/data/adapter.min.js" charset="utf-8"></script>
  </head>
  ```

## 4、页面中使用

```html
<template>
  <div class="ev-player">
    <CommonDragWindow
      v-model="innerShow"
      :width="600"
      :height="400"
      :resize="true"
      :position="position"
    >
      <template v-slot:title>{{ title }}</template>
      <template #default>
        <video
          :id="`video-${equipId}`"
          autoplay
          width="100%"
          height="98%"
        ></video>
      </template>
    </CommonDragWindow>
  </div>
</template>

<script setup>
  import CommonDragWindow from "./CommonDragWindow.vue";
  import { getConfigList } from "@/api/common.js";
  import { ref, onMounted, watchEffect, watch, nextTick } from "vue";
  const show = defineModel({ type: Boolean, default: false });
  const props = defineProps({
    title: {
      type: String,
      default: "监控视频",
    },
    equipId: {
      type: [Number, String],
    },
  });
  const innerShow = ref(false);
  const position = ref({
    top: 500,
    left: 20,
  });
  let webRtcServer = null;
  watchEffect(() => {
    innerShow.value = show.value;
  });
  watch(
    () => innerShow.value,
    async (val) => {
      if (val) {
        const rtspStr = "rtsp://132.239.12.145:554/axis-media/media.amp";
        if (rtspStr) {
          await nextTick(); // 待dom加载完毕
          let videoDocument = document.getElementById("video");
          webRtcServer = new WebRtcStreamer(
            videoDocument,
            `http://${window.appConfig.localhost}:8000`
          );
          webRtcServer.connect(rtspStr, null, `rtptransport=tcp&timeout=60`);
        }
      } else {
        webRtcServer?.disconnect();
        webRtcServer = null;
      }
      show.value = val;
    }
  );
  onMounted(() => {});
</script>

<style scoped lang="scss">
  .ev-player {
    :deep(video) {
      width: 100%;
      height: calc(100% - 5px);
    }
  }
</style>
```
