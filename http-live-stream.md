---
description: 'HTTP Live Stream, also known as HLS.'
---

# HTTP Live Stream

#### Using Chrome Extensions

Sometimes you want to download a video you watch on the internet, maybe it's a cat video that you want to share to your friend. Not all website put a video in a downloadable format, HLS is one of them.

To download HLS videos, there are two chrome extensions that I recommend:

* [HLS Downloader](https://github.com/puemos/hls-downloader-web-extension): Download HLS video easily in `.ts` format
* [Stream Recorder](https://www.hlsloader.com/): Not only download, but you can also record HLS video to `.mp4` format



#### Using youtube-dl

Alternatively, you can download it with `youtube-dl`. Fortunately, this program not only support Youtube, like the name, but also a bunch of other sites. [Click to visit youtube-dl Github repository](https://github.com/ytdl-org/youtube-dl).

Let's say you found an interesting video on Youtube and want to download it, simply copy the URL, it will be something like this:

```text
https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

You can simply download this video using this commands. 

```text
youtube-dl https://www.youtube.com/watch\?v=dQw4w9WgXcQ
```

Notice that there is a difference in the url, before the `?` there is a `\` , this is called escaping. Simply because without it, the program can't understand the url correctly.



#### Encrypted HLS

HLS can be encrypted, for example with `AES-128`. For this, you can simply download the stream using  HLS Downloader extension.

In some case, encrypted stream caused the file unable to be played. To overcome this, you can record the stream with Stream Recorder extension, but in my experience the quality can differ a little to the original. 

But, if you want to decrypt the `.ts` file downloaded, here the step you can follow:

1. Download `ffmpeg`, [click to see their website](https://ffmpeg.org/).
2. Go to your stream and find the `m3u8` file. You can try `View Source` or open developer tool and look in `Network` tab on Google Chrome.
3.  Open the `m3u8` file and look into `EXT-X-KEY` section. You will see a `URI`, open the `URI` in browser and you will download the Encryption Key, rename it to `enc.key` \(any name will work\).
4. Edit the `URI` of the `EXT-X-KEY` section to `enc.key` \(or other name that you use\).
5. Edit the `m3u8` file. Look into the `EXTINF` section, it will have number following it. That number indicate the duration of the file. Sum all the `EXTINF` sections to know the total duration.
6. Delete all `EXTINF` sections and create a new `EXTINF` section with total duration following it.
7. Under that, put the name of the `.ts` file.
8. Put the `.ts`, `.key`, and `.m3u8` file in one directory.
9. Now try to play the `m3u8` file on a media player like VLC, you should be able to play it now.
10. To convert it to mp4, run this `ffmpeg` command:

```text
ffmpeg -protocol_whitelist file,tls,tcp,https,crypto -allowed_extensions ALL -i name_of_file.m3u8 -c copy name_of_file.mp4
```

