1. 安装 ffmpeg，配置环境变量

   > 参考地址：https://www.gyan.dev/ffmpeg/builds/

2. 安装 mediamtx_v1.8.5_windows_amd64，配置端口号，默认 rtsp 端口：8554。双击启动程序，用于转发来自 ffmpeg 的 rtsp 推流。

   > 下载地址：https://github.com/bluenviron/mediamtx/releases

3. 推流 cmd：

   > ffmpeg -re -stream_loop -1 -i temp.mp4 -c copy -rtsp_transport tcp -f rtsp rtsp://127.0.0.1:8554/stream

4. 使用 VLC Media player 中【打开网络串流】，输入 rtsp://127.0.0.1:8554/stream，即可显示视频。

   > 下载地址：https://get.videolan.org/vlc/3.0.21/win64/vlc-3.0.21-win64.exe

5. java 开发

- java 工程引入

```xml
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>1.7.25</version>
</dependency>
<dependency>
    <groupId>com.github.kokorin.jaffree</groupId>
    <artifactId>jaffree</artifactId>
    <version>2023.09.10</version>
</dependency>
```

- 主要代码

```java
import com.github.kokorin.jaffree.ffmpeg.FFmpeg;
import com.github.kokorin.jaffree.ffmpeg.UrlOutput;
import com.github.kokorin.jaffree.ffmpeg.UrlInput;
import com.github.kokorin.jaffree.ffmpeg.FFmpegResultFuture;

    // 录制视频流保存至文件
    String pathToSrc = "rtsp://localhost:8554/stream";//"output00.mp4";
    String pathToDst = "cut0000.mp4";
    FFmpeg ffmpeg = FFmpeg.atPath()
            .addInput(
                    UrlInput.fromUrl("rtsp://localhost:8554/stream")
                            .addArguments("-rtsp_transport", "tcp") //default UDP
                            // .setPosition(0, TimeUnit.SECONDS)
                            // .setDuration(5500, TimeUnit.SECONDS)
                            )
            // .setFilter(StreamType.VIDEO, "scale=1024:-1")
            .setOverwriteOutput(true)
            // -movflags faststart 参数告诉 ffmpeg 重组 MP4 文件 atoms，将 moov 放到文件开头
            .addArguments("-movflags", "faststart")
            .addOutput(
                    UrlOutput.toUrl(pathToDst)
                            // .setPosition(0, TimeUnit.SECONDS)
                            );

    FFmpegResultFuture future = ffmpeg.executeAsync();// 异步执行转码存储、开始录制rtsp实时视频流

    Thread.sleep(10_000);
    future.graceStop(); // 停止和结束操作

    Thread.sleep(1_000);
    System.out.println(future.get()); // 获取对象
```

- 注意

```java
// 并行计算过程中，需要记录执行的ffmpeg进程，并控制进程的销毁
private static Map<String, FFmpegResultFuture> map = new ConcurrentHashMap<>(8);
map.put(id, future);
```
