## 视频床-jsdeliver
- https://cdn.jsdelivr.net/gh/Ysnsn/video-cdn/001.m3u8
- https://cdn.jsdelivr.net/gh/lete114/CDN2/video/4.m3u8

| 属性 | 值 | 说明 |
| :--: | ---- | ---- |
| autoplay | autoplay | 如果出现该属性，则视频在就绪后马上播放 |
|   controls   |   controls   |   如果出现该属性，则向用户显示控件，比如播放按钮   |
|   height   |   pixels   |   设置视频播放器的高度   |
|   loop   |   loop   |   如果出现该属性，则当媒介文件完成播放后再次开始播放   |
|   muted   |   muted   |   规定视频的音频输出应该被静音.   |
|   poster   |   URL   |   规定视频下载时显示的图像，或者在用户点击播放按钮前显示的图像。   |
|   preload   |   preload   |   如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 “autoplay”，则忽略该属性。   |
|   src   |   url   |  要播放的视频的 URL    |
|    width  |   pixels   |    设置视频播放器的宽度  |


````
ffmpeg.exe -y -i 002.mp4 -vcodec copy -acodec copy -vbsf h264_mp4toannexb 002.ts
ffmpeg -i 002.ts -c copy -map 0 -f segment -segment_list 002.m3u8 -segment_time 4 002%03d.ts
````


````
<script src="https://cdn.jsdelivr.net/npm/hls.js"></script>
<video id="video" preload muted loop autoplay style="height: 100%;width: 100%;object-fit: cover;">
</video>
<script>
  var video = document.getElementById('video');
  var videoSrc = 'https://cdn.jsdelivr.net/gh/Ysnsn/video-cdn/001.m3u8';
  if (Hls.isSupported()) {
    var hls = new Hls();
    hls.loadSource(videoSrc);
    hls.attachMedia(video);
    hls.on(Hls.Events.MANIFEST_PARSED, function() {
      video.play();
    });
  }
</script>
````
