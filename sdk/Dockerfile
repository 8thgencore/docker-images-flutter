FROM ghcr.io/cirruslabs/android-sdk:34

LABEL org.opencontainers.image.source=https://github.com/8thgencore/docker-images-flutter
USER root

# Setup new user
RUN useradd -u 1000 -m -s /bin/bash user

ARG flutter_version

ENV FLUTTER_HOME=${HOME}/sdks/flutter \
    FLUTTER_VERSION=$flutter_version
ENV FLUTTER_ROOT=$FLUTTER_HOME

ENV PATH ${PATH}:${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin

RUN git clone --depth 1 --branch ${FLUTTER_VERSION} https://github.com/flutter/flutter.git ${FLUTTER_HOME}

RUN yes | flutter doctor --android-licenses \
    && flutter doctor \
    && flutter precache \
    && sdkmanager "--update" "--verbose" \
    && sdkmanager "build-tools;34.0.0" \
    && sdkmanager "platform-tools" \
    && sdkmanager "platforms;android-34" \
    && sdkmanager "extras;android;m2repository" "extras;google;google_play_services" "extras;google;m2repository" \
    && chown -R 1000:1000 ${FLUTTER_HOME}

RUN chmod -R a+w /opt/android-sdk-linux

USER 1000
