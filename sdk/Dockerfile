FROM ghcr.io/cirruslabs/android-sdk:34

LABEL org.opencontainers.image.source=https://github.com/8thgencore/docker-images-flutter
USER root

ENV ANDROID_HOME=${HOME}/android-sdk-linux \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    LANGUAGE=en_US:en

ENV ANDROID_SDK_ROOT=$ANDROID_HOME \
    PATH=${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/emulator

ARG flutter_version

ENV FLUTTER_HOME=${HOME}/sdks/flutter \
    FLUTTER_VERSION=$flutter_version
ENV FLUTTER_ROOT=$FLUTTER_HOME

ENV PATH ${PATH}:${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin

RUN git clone --depth 1 --branch ${FLUTTER_VERSION} https://github.com/flutter/flutter.git ${FLUTTER_HOME}

RUN yes | flutter doctor --android-licenses \
    && flutter config --android-sdk ${HOME}/android-sdk-linux \
    && flutter doctor \
    && chown -R 1000:1000 ${FLUTTER_HOME}
