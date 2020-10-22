## IEAD下Tomcat源码部署安装

### 导入tomcat源码
1. 创建home目录
2. 将conf webapps 目录移入home目录下
3. 创建pom.xml文件,引入tomcat依赖包
4. 在IDEA中导入工程
5. 配置IDEA的启动类
  + 注意：`E:/projects/itcast_project_tomcat/apache-tomcat-8.5.42-src`是当前项目目录
    ```properites
        -Dcatalina.home-E:/projects/itcast_project_tomcat/apache-tomcat-8.5.42-src/home
        -Dcatalina.base=E:/projects/itcast_project_tomcat/apache-tomcat-8.5.42-src/home
        -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
        -Djava.utilelogging.config.file=E:/projects/itcast_project_tomcat/apache-tomcat-8.5.42-src/home/conf/logging.properties
    ```


### IDEA编译java提示找不到符号
+ 首先查看maven设置，不要使用默认的maven版本：
+ Maven-Reimport
+ File Encodings 设置为utf-8
+ 重启IDEA

### 解决Tomcat源码导入eclipse后， CookieFilter类找不到
+ 将以下代码添加到tomcat util包下
```java
/*
 * Licensed to the Apache Software Foundation (ASF) under one or more
 * contributor license agreements.  See the NOTICE file distributed with
 * this work for additional information regarding copyright ownership.
 * The ASF licenses this file to You under the Apache License, Version 2.0
 * (the "License"); you may not use this file except in compliance with
 * the License.  You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package util;

import java.util.Locale;
import java.util.StringTokenizer;

/**
 * Processes a cookie header and attempts to obfuscate any cookie values that
 * represent session IDs from other web applications. Since session cookie names
 * are configurable, as are session ID lengths, this filter is not expected to
 * be 100% effective.
 *
 * It is required that the examples web application is removed in security
 * conscious environments as documented in the Security How-To. This filter is
 * intended to reduce the impact of failing to follow that advice. A failure by
 * this filter to obfuscate a session ID or similar value is not a security
 * vulnerability. In such instances the vulnerability is the failure to remove
 * the examples web application.
 */
public class CookieFilter {

    private static final String OBFUSCATED = "[obfuscated]";

    private CookieFilter() {
        // Hide default constructor
    }

    public static String filter(String cookieHeader, String sessionId) {

        StringBuilder sb = new StringBuilder(cookieHeader.length());

        // Cookie name value pairs are ';' separated.
        // Session IDs don't use ; in the value so don't worry about quoted
        // values that contain ;
        StringTokenizer st = new StringTokenizer(cookieHeader, ";");

        boolean first = true;
        while (st.hasMoreTokens()) {
            if (first) {
                first = false;
            } else {
                sb.append(';');
            }
            sb.append(filterNameValuePair(st.nextToken(), sessionId));
        }


        return sb.toString();
    }

    private static String filterNameValuePair(String input, String sessionId) {
        int i = input.indexOf('=');
        if (i == -1) {
            return input;
        }
        String name = input.substring(0, i);
        String value = input.substring(i + 1, input.length());

        return name + "=" + filter(name, value, sessionId);
    }

    public static String filter(String cookieName, String cookieValue, String sessionId) {
        if (cookieName.toLowerCase(Locale.ENGLISH).contains("jsessionid") &&
                (sessionId == null || !cookieValue.contains(sessionId))) {
            cookieValue = OBFUSCATED;
        }

        return cookieValue;
    }
}
```

 