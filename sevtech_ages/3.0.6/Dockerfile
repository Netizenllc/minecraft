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
	wget --no-check-certificate https://media.forgecdn.net/files/2550/81/SevTech_Ages_Server_3.0.6.zip && \
	unzip SevTech_Ages_Server_3.0.6.zip && \
	rm SevTech_Ages_Server_3.0.6.zip && \
	chmod u+x Install.sh ServerStart.sh && \
	echo "#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt && \
	echo "$(date)" >> eula.txt && \
	echo "eula=TRUE" >> eula.txt && \
	chown -R minecraft:minecraft /minecraft
USER minecraft

# Running install
RUN /minecraft/Install.sh

# Expose port 25565
EXPOSE 25565

# Expose volume
VOLUME ["/minecraft/world"]

# Start server
CMD ["/bin/bash", "/minecraft/ServerStart.sh"]
