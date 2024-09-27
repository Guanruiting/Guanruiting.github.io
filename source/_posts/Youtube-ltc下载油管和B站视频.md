---
title: 'Youtube-ltc下载油管和B站视频'
date: 2021-01-09 22:31:00
tags:
- Tools
categories: 中文
---

Youtube-lt是一个用Python开发的命令行下载工具，支持下载youtube、Bilibili等网站的视频。

## 安装

**UNIX** (Linux, macOS, etc.)  
使用 wget:

```bash
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```

使用 curl:

```bash
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```

**Windows** 用户可以通过下载 [youtube-dlc.exe](https://github.com/blackjack4494/yt-dlc/releases/latest/download/youtube-dlc.exe) 进行安装 (**不要** 安装在 `C:\Windows\System32`!).

## 使用

使用方式非常简单，在终端/命令行执行：

```cmd
youtube-dl [OPTIONS] URL [URL...]
// 示例（使用代理）
youtube-dl https://www.youtube.com/watch?v=5giYv5n616E --proxy 127.0.0.1:19180
```

## OPTIONS

youtube-dlc功能强大，提供了非常多的设置选项，我们可以通过options设置各种参数。

- 下载多个地址

  希望从其他网站下载多个视频，如果是这样，用空格分隔视频网址 `$ youtube-dl <url1> <url2>`；

  将链接全部放在文本文件中，并将其作为参数传递给Youtube-dl，`$ youtube-dl -a url.txt`，此命令将下载url.txt文件中提到的所有视频。

- 设置代理

  通过`--proxy URL`代理选项，支持设置http或sock代理：

  ```bash
  youtube-dl --proxy socks5://127.0.0.1:1080 url
  ```

  如果要将代理用于所有其他调用，请创建一个配置文件

  Linux / OSX：〜/ .config / youtube-dl / config

  Windows：％APPDATA％\\ youtube-dl \\ config.txt

  文件内容示例：

  ```bash
  --proxy socks5://127.0.0.1:1080
  ```

- 下载指定格式视频

  `-F` 查看所有视频格式，下载指定质量的视频和音频并自动合并：  `youtube-dl -f [format code] [url]`

  ```bash
  youtube-dl -f 247+251 https://www.youtube.com/watch?v=UyJ8Qbh_LH0
  # or
  youtube-dl -f bestvideo+bestaudio https://www.youtube.com/watch?v=UyJ8Qbh_LH0
  ```

  YouTube 的 1080p 及以上的分辨率都是音视频分离的，需要分别下载视频和音频，命令可以使用 `247+251` （或 `bestvideo+bestaudio`）这样的组合，如果系统中安装了 FFmpeg 的话 , youtube-dl 会自动合并下下好的视频和音频, 然后自动删除单独的音视频文件:通过免输入的批处理脚本和 shell 脚本下载YouTube高清视频，参考《使用 Youtube-dl 下载 Youtube 1080P+ 视频》：https://chengww.com/archives/youtube_download.html#What-is-it

  PS：FFmpeg也是一个非常强大的命令行工具，可以记录、转换和传输音频/视频。Mac安装FFmpeg视频教程：https://youtu.be/8nbuqYw2OCw

  FFmpeg usage: ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...

  ```bash
  brew install ffmpeg
  clear
  ffmpeg -h
  ffmpeg -i input.avi  output.mp4
  ```

- 下载视频中的音频

  Youtube-dl允许我们仅从Youtube视频下载音频，默认情况下，Youtube-dl将以Ogg（opus）格式下载音频。如果想下载任何其他格式，例如mp3，以下命令将从给定视频下载音频，将其转换为MP3并将其保存在当前目录中：

  ```bash
  youtube-dl -x --audio-format mp3 https://www.youtube.com/watch?v=7E-cwdnsiow
  ```

  PS：转换音频格式需要安装ffmpeg或avconv。

- 下载字幕

  下载字幕，并按顺序选择 ass/srt/best 字幕，把字幕转成 srt 格式

  ```bash
  youtube-dl --write-sub --sub-format "ass/srt/best" --convert-subs "srt" "video_url"
  ```

  `—write-sub`：写入字幕，即把字幕下载。  
  `--sub-format`：指定字幕格式，按顺序选，不存在则选下一个。  
  `--convert-subs`： 转换字幕，格式有限制，通用为 srt ；若不转，某些字幕可能是 .vtt 的；如果有 ass 字幕可下载，则无须加此项。

  ```bash
  youtube-dl --proxy 127.0.0.1:19180 --write-sub --sub-format "ass/srt/best" --convert-subs "srt" https://www.youtube.com/watch?v=Q63qjIXMqwU&t=2s
  ```

  

- 自定义文件名称

  ```bash
  # 自定义视频名称
  youtube-dl -o 'some name' https://www.youtube.com/watch?v=7E-cwdnsiow
  # 下载播放列表并重命名文件
  youtube-dl -o "%(playlist_index)s.%(title)s-%(id)s.%(ext)s" PLAYLIST_URL 
  ```

- 使用登陆账户下载

  ```bash
  youtube-dl -u USERNAME -p PASSWORD UDEMY-Course-URL
  ```

  

  