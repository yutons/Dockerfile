FROM alpine:latest

MAINTAINER yutons <yuton.yao@qq.com>

# 更换Alpine源为mirrors.huaweicloud.com
RUN echo https://mirrors.huaweicloud.com/alpine/v3.8/main > /etc/apk/repositories && \
    echo https://mirrors.huaweicloud.com/alpine/v3.8/community >> /etc/apk/repositories
RUN apk update && apk upgrade

# 解决Docker部署openjdk后无字体空指针异常
RUN set -xe && apk --no-cache add ttf-dejavu fontconfig

# 解决Docker openjdk-8-jdk-alpine 容器时间与jdk时区不同问题(https://www.cnblogs.com/solooo/p/7832117.html)
ADD localtime /etc/
RUN echo "Asia/Shanghai" > /etc/timezone

#******************设置JAVA变量环境******************
RUN cd /usr/local && mkdir jdk
ENV JAVA_HOME=/usr/local/jdk
ENV CLASSPATH=$JAVA_HOME/bin
ENV PATH=$PATH:$JAVA_HOME/bin
CMD ["java","-version"]