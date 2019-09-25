---
layout: post
title: Spring Boot + Gradle + Apache Tiles 적용 방법
excerpt: ""
categories: [Spring]
comments: true
---

## Spring Boot + Gradle + Apache Tiles 적용 방법

<br/>

### 먼저 build.gradle에 아래 두 개를 설정한다.
```gradle
dependencies {
	....
	//Apache Tiles
	compile("org.apache.tiles:tiles-jsp:3.0.8")
	compile("javax.servlet:jstl:1.2")
}
```

<br/>

### WebMvcConfigurer를 상속받는 TilesConfig class를 만든다.
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ViewResolverRegistry;
import org.springframework.web.servlet.view.tiles3.TilesConfigurer;
import org.springframework.web.servlet.view.tiles3.TilesViewResolver;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class TilesConfig implements WebMvcConfigurer {

    @Bean
    public TilesConfigurer tilesConfigurer() {
        TilesConfigurer configurer = new TilesConfigurer();
        configurer.setDefinitions(new String[]{"/WEB-INF/tiles/tiles.xml"});
        configurer.setCheckRefresh(true);
        return configurer;
    }

    @Override
    public void configureViewResolvers(ViewResolverRegistry registry) {
        TilesViewResolver viewResolver = new TilesViewResolver();
        registry.viewResolver(viewResolver);
    }
}
```

<br/>

### WEB-INF > tiles > layout 아래 기본 jsp를 생성한다.
![Smithsonian Image](/img/2019/190925/1.tree.jpg)


<br/>

### tiles.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE tiles-definitions PUBLIC 
        "-//Apache Software Foundation//DTD Tiles Configuration 3.0//EN"
        "http://tiles.apache.org/dtds/tiles-config_3_0.dtd">
<tiles-definitions>
    <!-- Header / Footer가 제외된 화면 -->
    <definition name="default" template="/WEB-INF/tiles/layout/default.jsp">
        <put-attribute name="body" value="" />
    </definition>

    <definition name="error/*" extends="default">
        <put-attribute name="body" value="/WEB-INF/view/error/{1}.jsp" />
    </definition>

    <definition name="login" extends="default">
        <put-attribute name="body" value="/WEB-INF/view/login.jsp" />
    </definition>

    <!-- Header / Footer가 들어간 기본 화면 -->
    <definition name="main" template="/WEB-INF/tiles/layout/main.jsp">
        <put-attribute name="header" value="/WEB-INF/tiles/layout/header.jsp" />
        <put-attribute name="body" value="" />
        <put-attribute name="footer" value="/WEB-INF/tiles/layout/footer.jsp" />
    </definition>

    <definition name="*/*" extends="main">
        <put-attribute name="body" value="/WEB-INF/view/{1}/{2}.jsp" />
    </definition>
</tiles-definitions>
```

<br/>

### main.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://tiles.apache.org/tags-tiles" prefix="tiles"%>
<!DOCTYPE html>
<html lang="ko">
<head>
</head>
<body>
    <tiles:insertAttribute name="header"/>
    <tiles:insertAttribute name="body"/>
    <tiles:insertAttribute name="footer"/>
</body>
</html>
```

<br/>

### header.jsp, footer.jsp
```jsp
//header.jsp
<div>tiles header</div>

//footer.jsp
<div>tiles footer</div>
```

<br/>

### default.jsp (header / footer가 없는 기본 페이지일 경우)
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://tiles.apache.org/tags-tiles" prefix="tiles"%>
<!DOCTYPE html>
<html lang="ko">
<head>
</head>
<body>
    <tiles:insertAttribute name="body"/>
</body>
</html>
```

<br/>

### main 호출 Controller.java
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/")
public class TestController {
    private static final Logger log = LoggerFactory.getLogger(TestController.class);

    @RequestMapping("/main")
    public String main(){
        log.info("####main#####");
        return "main/index";
    }
}
```

