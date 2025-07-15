FROM openjdk:8-jre-slim

# ForgeとMinecraftのバージョンを環境変数で定義
ENV FORGE_VERSION=14.23.5.2860
ENV MC_VERSION=1.12.2
ENV INSTALLER=forge-${MC_VERSION}-${FORGE_VERSION}-installer.jar
ENV FORGE_JAR=forge-${MC_VERSION}-${FORGE_VERSION}.jar

WORKDIR /server

# wgetをインストール（Forgeのダウンロードに必要）
RUN apt-get update && \
    apt-get install -y wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Forgeが未インストールの場合のみインストール
RUN if [ ! -f "${FORGE_JAR}" ]; then \
    echo "Downloading Forge installer..." && \
    wget -O ${INSTALLER} https://maven.minecraftforge.net/net/minecraftforge/forge/${MC_VERSION}-${FORGE_VERSION}/${INSTALLER} && \
    java -jar ${INSTALLER} --installServer && \
    rm ${INSTALLER}; \
    else \
    echo "Forge already installed. Skipping installation."; \
    fi

# EULA に同意
RUN echo "eula=true" > eula.txt

EXPOSE 25565

CMD ["java", "-Xmx2G", "-Xms1G", "-jar", "forge-1.12.2-14.23.5.2860.jar", "nogui"]
