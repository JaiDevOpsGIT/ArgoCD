FROM node:16-alpine

# Install Docker and Docker-in-Docker (dind)
RUN apk add --no-cache docker \
    && curl -fsSL https://get.docker.com/ | sh \
    && apk add --no-cache bash

# Ensure Docker is installed
RUN docker --version

# Install dependencies
RUN apk add --no-cache openjdk11 bash unzip curl

# Install Apache Ant 1.10.13
RUN wget https://downloads.apache.org/ant/binaries/apache-ant-1.10.13-bin.tar.gz && \
    tar -xzf apache-ant-1.10.13-bin.tar.gz -C /opt/ && \
    ln -s /opt/apache-ant-1.10.13/bin/ant /usr/local/bin/ant

# Install Android SDK
RUN mkdir -p /opt/android-sdk && \
    curl -o commandlinetools-linux.zip https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip && \
    unzip commandlinetools-linux.zip -d /opt/android-sdk/cmdline-tools && \
    mv /opt/android-sdk/cmdline-tools/cmdline-tools /opt/android-sdk/cmdline-tools/latest

# Set environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk
ENV ANT_HOME=/opt/apache-ant-1.10.13
ENV ANDROID_HOME=/opt/android-sdk
ENV PATH="${PATH}:${ANT_HOME}/bin:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools"

# Verify installations
RUN java -version && ant -version