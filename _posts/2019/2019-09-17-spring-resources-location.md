---
layout: post
title: Spring boot에서 외부 경로 매핑하기
excerpt: "프로젝트 외부 폴더 경로 매핑 방법"
categories: [Spring]
comments: true
---

## Spring boot에서 외부 경로 매핑하기

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebMvcConfig implements WebMvcConfigurer {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/video_view/**")
                .addResourceLocations("file:/DATA/video/"); //리눅스 root에서 시작하는 폴더 경로
    }
}
```

<br/>

```java
//윈도우일 경우 아래처럼 사용하면 된다.
addResourceLocations("file:///D:/DATA/video/");
```