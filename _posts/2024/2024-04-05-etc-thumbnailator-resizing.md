---
layout: post
title: thumbnailator + Java 이미지 리사이징 (썸네일)
excerpt: ""
categories: [ETC]
comments: true
---

Java에서 이미지 리사이징(썸네일 등)을 위한 방법이다.  
build.gradle에 아래 내용을 작성한다.

```bash
dependencies {
    implementation group: 'net.coobird', name: 'thumbnailator', version: '0.4.20'
}
```

<br/>
<br/>

```java
import net.coobird.thumbnailator.Thumbnails;
import net.coobird.thumbnailator.name.Rename;
import java.io.File;

import lombok.extern.slf4j.Slf4j;

@Slf4j
public class ThumbnailProcess {

	public static void convert() {
		String root = "src/main/resources/static";
		String output_path = root + "/thumbnails";
		String originalFilename = "input.png";
		File destinationDir = new File(output_path);

		log.info(root + "/" + File.separator + originalFilename);
		
		try {
			if(!destinationDir.exists()) {
				destinationDir.mkdirs();
			}
			Thumbnails.of(new File(root + "/" + File.separator + originalFilename))
				.size(70, 150)
				.toFiles(destinationDir, Rename.NO_CHANGE);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```