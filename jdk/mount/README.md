# openjdk问题及解决方案

## 问题

### 问题1:问题来源:使用openjdk:8-jre-alpine部署web服务,图片验证码无法正常显示

```
# 解决Docker部署openjdk后无字体空指针异常
RUN set -xe && apk --no-cache add ttf-dejavu fontconfig
```

### 问题2:问题来源:openjdk默认UTC时间,需将容器时间与宿主时间进行同步

```
#[解决Docker openjdk-8-jdk-alpine 容器时间与jdk时区不同问题](https://www.cnblogs.com/solooo/p/7832117.html)
ADD localtime /etc/ && RUN echo "Asia/Shanghai" > /etc/timezone
```

## 部署

### 部署脚本

```
docker build -t yutons/openjdk:8-jre-font-alpine . && docker rmi $(docker images -f "dangling=true" -q)
```

## 运行

### 运行挂在jdk
```
# 前提：宿主机需正常安装jdk
# 正确挂载jdk路径
docker run 
-v /usr/local/jdk1.8.0_161:/usr/local/jdk  
--name mountjdk mountjdk
```