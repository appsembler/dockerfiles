FROM kdelfour/supervisor-docker
MAINTAINER Brian Dant <brian@appsembler.com>

RUN apt-get update 
RUN apt-get install -y build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs maven

# Make sh recognize scripts
RUN rm /bin/sh && ln -snf /bin/bash /bin/sh

# ------------------------------------------------------------------------------
# Install Orion 
RUN mkdir /orion
WORKDIR /orion

RUN git clone https://github.com/eclipse/orion.client.git
RUN git clone https://github.com/eclipse/orion.server.git
WORKDIR /orion/orion.server 
RUN mvn clean install -P platform-kepler,local-build -Dorion.client.build.skip -DskipTests

# ------------------------------------------------------------------------------
# Add supervisord conf
ADD conf/orion-maven.conf /etc/supervisor/conf.d/

# ------------------------------------------------------------------------------
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 8080

# ------------------------------------------------------------------------------
# Start supervisor, define default command.
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
