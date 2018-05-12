FROM java:8-jre

MAINTAINER Wesley Shoffner (NetizenLLC) (https://github.com/NetizenLLC)
# Based on a docker file by jonasbonno

# Updating container
RUN apt-get -y update && \
        apt-get upgrade --yes --force-yes && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

# Setting workdir
WORKDIR /minecraft

# Changing user to root
USER root

# Creating user and downloading files
RUN useradd -m -U minecraft && \
        mkdir -p /minecraft/world && \
        wget --no-check-certificate https://media.forgecdn.net/files/2555/817/Modern+Skyblock-3.3.1.4+Server+File.zip && \
        unzip Modern+Skyblock-3.3.1.4+Server+File.zip && \
        rm Modern+Skyblock-3.3.1.4+Server+File.zip && \
        echo "#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt && \
        echo "$(date)" >> eula.txt && \
        echo "eula=TRUE" >> eula.txt && \
        chown -R minecraft:minecraft /minecraft
USER minecraft

# Expose port 25565
EXPOSE 25565

# Expose volume
VOLUME ["/minecraft/world"]

# Start server
CMD ["/bin/bash", "java -Xmx1024M -Xms1024M -jar /minecraft/forge-1.12.2-14.23.3.2670-universal.jar"]
