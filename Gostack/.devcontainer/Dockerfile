FROM node:lts

#Variaveis de Ambiente
ENV DEBIAN_FRONTEND=noninteractive \
    JAVA_VERSION=8 \
    GRADLE_VERSION=6.5 \
    BUILD_TOOLS=28.0.3 \
    PLATAFORMS=android-28 \
    ANDROID_HOME=/opt

#Dependencias 
RUN apt update -y &&\
    apt upgrade -y &&\
    apt install -y apt-utils &&\
    apt install curl unzip zip -y &&\
    apt install openjdk-"$JAVA_VERSION"-jdk -y &&\
    export JAVA_HOME=/usr/lib/jvm/java-$JAVA_VERSION-openjdk-amd64 &&\
    apt install -y git wget curl unzip build-essential ruby ruby-dev ruby-ffi gcc make && \
    gem install sass &&\
    git config --global user.email "you@example.com" &&\
    git config --global user.name "Your Name"

# SDK Tools
RUN cd /opt &&\
    wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip &&\
    unzip sdk-tools-linux-4333796.zip &&\
    rm -f sdk-tools-linux-4333796.zip &&\
    chown -R root. /opt

# Config Plataforms
RUN yes | /opt/tools/bin/sdkmanager --include_obsolete platform-tools "platform-tools" "platforms;$PLATAFORMS" "build-tools;$BUILD_TOOLS" 

# Install Gradle
RUN wget https://services.gradle.org/distributions/gradle-"$GRADLE_VERSION"-bin.zip && \
    mkdir /opt/gradle && \
    unzip -d /opt/gradle gradle-"$GRADLE_VERSION"-bin.zip && \
    rm -rf gradle-"$GRADLE_VERSION"-bin.zip

# Sentando varaveis no PATH
ENV PATH ${PATH}:/opt/platform-tools:/opt/tools:/opt/gradle/gradle-"$GRADLE_VERSION"/bin

# Clean up
RUN apt-get clean
RUN apt-get purge
    
RUN npm i -g create-react-app 
RUN npm i -g react-native-cli

WORKDIR /home/