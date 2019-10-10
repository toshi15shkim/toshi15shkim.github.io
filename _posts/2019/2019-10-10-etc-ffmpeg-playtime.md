---
layout: post
title: FFMPEG + Java 동영상 재생 시간 구하기
excerpt: "리눅스에 ffmpeg이 설치되어 있다는 가정"
categories: [ETC]
comments: true
---

Java에서 동영상 재생시간을 가져오기 위한 방법이다.  
build.gradle에 아래 내용을 작성한다.

```bash
dependencies {
    compile group: 'net.bramp.ffmpeg', name: 'ffmpeg', version: '0.6.2'
}
```

<br/>
<br/>

```java
import java.io.IOException;

import net.bramp.ffmpeg.FFprobe;
import net.bramp.ffmpeg.probe.FFmpegFormat;
import net.bramp.ffmpeg.probe.FFmpegProbeResult;

public class VodEncoder {
    /**
    * 동영상 플레이타임을 가져오는 메소드
    */
    public static String media_player_time(String vod_upload_path, String fileName) {
        log.info("@@ media_player_time start @@");
        String returnData = "0";

        try {
            FFprobe ffprobe = new FFprobe("/DATA/ffmpeg/ffprobe");  //리눅스에 설치되어 있는 ffmpeg 폴더
            FFmpegProbeResult probeResult = ffprobe.probe(vod_upload_path + "/" + fileName);
            FFmpegFormat format = probeResult.getFormat();
            double second = format.duration;    //초단위

            returnData = second+"";

        } catch(IOException e) {
            log.error("@@ media_player_time error @@", e);
        } finally {
            log.info("@@ media_player_time end @@");
        }

        return returnData;
    }
}
```