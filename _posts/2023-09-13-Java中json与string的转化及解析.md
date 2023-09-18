---
layout:     post
title:      Java中json与string的转化及解析
subtitle:   
date:       2023-09-18
author:     znx
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Java
    - Json

---



json转string后 string转List：

```java
        JsonObject socketObj = new JsonObject();
        socketObj.addProperty("equipmentNo", "1");
        socketObj.addProperty("equipmentType", "2");
        String request = socketObj.toString();
        List<String> listStr = Arrays.asList(request);
        String equipmentNo = listStr.get(0);
        System.out.println("equipmentNo: " + equipmentNo);
```



结果如下：

![image-20230918141536604](/Users/znx/Library/Application Support/typora-user-images/image-20230918141536604.png)



可以看出 string转list 和前面json转string一点关系也没有

正确如下：

```java
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
 
JsonObject socketObj = new JsonObject();
socketObj.addProperty("equipmentNo", "1");
socketObj.addProperty("equipmentType", "2");
String socket2String = socketObj.toString();
JsonParser parser = new JsonParser();
JsonObject requestObj = parser.parse(socket2String).getAsJsonObject();
 
String equipmentNo = requestObj.get("equipmentNo").getAsString();
String equipmentType = requestObj.get("equipmentType").getAsString();
 
System.out.println("equipmentNo: " + equipmentNo);
System.out.println("equipmentType: " + equipmentType);
```



![image-20230918141701177](/Users/znx/Desktop/github/znx-blog/image/work/1/1-3.png)

用google的jsonParser import com.google.gson.JsonParser 即可
