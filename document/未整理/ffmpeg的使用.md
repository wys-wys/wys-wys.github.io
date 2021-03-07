# windows安装ffmpeg提取视频帧

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[nyj_ouc](https://me.csdn.net/nyj_ouc) 2020-04-26 14:57:00 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 97 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

版权

在windows下用pip install ffmpeg，显示安装成功，但使用时报错，显示
‘ffmpeg’ 不是内部或外部命令,也不是可运行的程序

到官网上下载安装包，不需要运行，直接写入环境变量
点击桌面我的计算机图像，右键属性，再点击右侧的高级系统设置，点击右下角的环境变量，出来两个变量，上面的是用户变量，下面的是系统变量，在下面的是系统变量中找到path，点击编辑，直接在后面加上一个分号`；`，再把ffemeg的路径加上去，再确定就ok了,写入环境变量[参考](https://blog.csdn.net/ChinarCSDN/article/details/78667262)

参考[安装ffmpeg](https://blog.csdn.net/qq_37665834/article/details/82936733?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1&utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1)
不过这个链接只提取一张图片，我是要提取多张图片，因此需要参考另一个[博客](https://blog.csdn.net/zhzhanp/article/details/50775101?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1&utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1)
这里直接给出命令

```python
ffmpeg -i C:\Users\michael\Desktop\my.mp4 -q:v 2 -f  image2 C:\Users\michael\Desktop\output-images\%07d.jpg
1
```

其中`C:\Users\michael\Desktop\my.mp4`是我的输入视频的路径及名称，`C:\Users\michael\Desktop\output-images\`是我输出图片的路径，图片保存在`output-images`文件夹中，`，`image2`这个参数不需要动，`%07d.jpg`中的07指的是图片的命名有7位数，从0000001.jpg开始命名

```python
ffmpeg -i C:\Users\michael\Desktop\my.mp4 -q:v 2 -r 1 -f  image2 C:\Users\michael\Desktop\output-images\%07d.jpg
1
```

-r`从视频中每秒钟抽取图片的数量

```python
ffmpeg -i C:\Users\michael\Desktop\my.mp4 -q:v 2 -r 1 -f  image2 C:\Users\michael\Desktop\output-images\%07d.jpg
1
```

-vframes 指定抽取的帧数,如果为5，表示只抽前面5的张图片

# [FFMPEG 常用命令行](https://www.cnblogs.com/standardzero/p/10823407.html)



目录

- [1. 分离音视频](https://www.cnblogs.com/standardzero/p/10823407.html#1-分离音视频)
- [2. 解复用](https://www.cnblogs.com/standardzero/p/10823407.html#2-解复用)
- [3. 视频转码](https://www.cnblogs.com/standardzero/p/10823407.html#3-视频转码)
- [4. 视频封装](https://www.cnblogs.com/standardzero/p/10823407.html#4-视频封装)
- [5. 视频剪切](https://www.cnblogs.com/standardzero/p/10823407.html#5-视频剪切)
- [6. 视频录制](https://www.cnblogs.com/standardzero/p/10823407.html#6-视频录制)
- [7.叠加水印](https://www.cnblogs.com/standardzero/p/10823407.html#7叠加水印)
- [8.将MP3转换为PCM数据](https://www.cnblogs.com/standardzero/p/10823407.html#8将mp3转换为pcm数据)
- [9. 推送RTP流、接收RTP流并存为ts文件](https://www.cnblogs.com/standardzero/p/10823407.html#9-推送rtp流、接收rtp流并存为ts文件)
- [10. ffmpeg 编码](https://www.cnblogs.com/standardzero/p/10823407.html#10-ffmpeg-编码)
- [11. ffmpeg 解码](https://www.cnblogs.com/standardzero/p/10823407.html#11-ffmpeg-解码)
- [12. 截取 YUV](https://www.cnblogs.com/standardzero/p/10823407.html#12-截取-yuv)
- [13. 压缩分辨率](https://www.cnblogs.com/standardzero/p/10823407.html#13-压缩分辨率)
- [14. ffplay 播放YUV](https://www.cnblogs.com/standardzero/p/10823407.html#14-ffplay-播放yuv)
- [15. ffplay 播放PCM](https://www.cnblogs.com/standardzero/p/10823407.html#15-ffplay-播放pcm)
- [16. 将 PCM 数据编码为 AC3](https://www.cnblogs.com/standardzero/p/10823407.html#16-将-pcm-数据编码为-ac3)



# 1. 分离音视频

- 分离视频：`ffmpeg -i test.mkv -vcodec copy -an test_video.mp4`
- 分离音频：`ffmpeg -i test.mkv -acodec copy -vn test_audio.mp2`

# 2. 解复用

```
ffmpeg –i test.mp4 –vcodec copy –an –f m4v test.264
ffmpeg –i test.avi –vcodec copy –an –f m4v test.264
```

# 3. 视频转码

```
ffmpeg -i test.mp4 -vcodec h264 -s 480*480 -an -f m4v test.264
ffmpeg –i test.mp4 –vcodec h264 –bf 0 –g 25 –s 352*278 –an –f m4v test.264
```

**说明**: -bf B帧数目控制，-g 关键帧间隔控制，-s 分辨率控制

# 4. 视频封装

```
ffmpeg –i test_video.mp4 –i test_audio.mp2 –vcodec copy –acodec copy test.mkv
```

# 5. 视频剪切

**提取图片**：`ffmpeg –i test.avi –r 1 –f image2 image-%3d.jpeg`

**剪切视频**：

剪切从0:1:30开始时长20s的视频

```
ffmpeg -ss 0:1:30 -t 0:0:20 -i input.avi -vcodec copy -acodec copy output.avi
```

剪切从0:1:30开始到0:2:30秒间的视频

```
ffmpeg -i input.avi -vcodec copy -acodec copy -ss 0:1:30 -to 0:2:30 output.avi
```

# 6. 视频录制

```
ffmpeg –i rtsp://192.168.3.205:5555/test –vcodec copy out.avi
```

# 7.叠加水印

**使用命令**：`ffmpeg -i Titanic.mkv -vf "movie=test.PNG,scale=100:150[watermask];[in][watermask] overlay=100:100[out]" -y Titanic.mp4`

`scale`：水印的大小

`overlay`：水印的位置

# 8.将MP3转换为PCM数据

```
ffmpeg -i test.mp3 -f s16be -ab 192 -ar 44100 test.pcm
```

# 9. 推送RTP流、接收RTP流并存为ts文件

- 推送RTP流

```
ffmpeg -re -i 4kp30_avc.mp4 -an -c copy -f rtp rtp://192.168.25.89:5004 > rtp.sdp
```

- ffplay 接收rtp流

```
ffplay.exe -protocol_whitelist "udp,tcp,http,https,file,rtp" rtp.sdp
```

- ffmpeg 接收rtp流，并存为ts文件

```
ffmpeg -protocol_whitelist "udp,tcp,http,https,file,rtp" -i rtp.sdp -c copy 4kp30_avc.ts
```

# 10. ffmpeg 编码

```
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec mpeg4 bus_cif.avi//avi
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec mpeg2video bus_cif.VOB//dvd
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec wmv1 bus_cif.wmv//wmv
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec h264 bus_cif.mp4//mp4
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec flv bus_cif.flv//flv
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec rv10 bus_cif.rm//rm
ffmpeg -s 352*288 -pix_fmt yuv420p -i bus_cif.yuv -vcodec vp9 bus_cif.webm//webm
```

# 11. ffmpeg 解码

```
ffmpeg -i test1.h264 -c:v rawvideo -pix_fmt yuv420p test1.yuv
```

# 12. 截取 YUV

**从第0帧开始截取30帧**

```
ffmpeg -s widthxheight -i input.yuv -c:v rawvideo -filter:v select="between(n\, 0\, 29)" out.yuv
```

**根据时间截取帧(截取从第10秒到第20秒)**

```
ffmpeg -s widthxheight -i input.yuv -c:v rawvideo -filter:v select="between(t\, 10\, 20)" out.yuv
```

# 13. 压缩分辨率

```
ffmpeg -i 1080_60i.ts -s 720x576 720x576.ts
```

# 14. ffplay 播放YUV

```
ffplay -f rawvideo -video_size 1280x720 -pix_fmt nv12  test.yuv
需要指定的参数:
1. -video_size 指定yuv的宽高
2. -pix_fmt 指定yuv的格式
yuv的格式名可以通过 ffplay -pix_fmts来查询
```

# 15. ffplay 播放PCM

```
ffplay -ar 44100 -channels 1 -f s16le -i test.pcm
需要指定的参数:
1. -ar pcm的采样率
2. -channels pcm的通道数
3. -f pcm的格式
pcm的格式可以通过ffplay -sample_fmts来查询
```

# 16. 将 PCM 数据编码为 AC3

```
ffmpeg -y -f s16le -ac 1 -ar 44100 -acodec pcm_s16le -i audio_1.pcm test.ac3
```