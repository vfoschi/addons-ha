ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH

WORKDIR /opt/runzero

# Ensure curl is available and install tools for wireless scanning.
#
RUN apt update && apt install -y curl wireless-tools

# Install Chrome for screenshots.
#
#RUN curl -o chrome.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
#    apt install -y ./chrome.deb

# Set AGENT_URL to be the download URL for your Linux runZero Explorer. To 
# find your URL, go to https://console.runzero.com/deploy/download/explorers 
# and click on the first URL box to copy it to the clipboard.
#
ENV AGENT_URL=https://console.rumble.run/download/explorer/DT23B7E338AB5A68146F2D89D2C1C6/58f59159/runzero-explorer-linux-${BUILD_ARCH}.bin 

# This ID is used to track the Explorer even if the container is rebuilt.
# Set it to a unique 32 character hex ID. You can generate one via:
#
# $ openssl rand -hex 16
#
ENV RUNZERO_AGENT_HOST_ID=cccc457f746295a846cba351121c1de9

# If you need to set environment variables to change the Explorer behavior,
# you can do so via the ENV directive. Example:
#
# ENV RUNZERO_AGENT_LOG_DEBUG=true

ADD https://console.rumble.run/download/explorer/DT23B7E338AB5A68146F2D89D2C1C6/58f59159/runzero-explorer-linux-${BUILD_ARCH}.bin  runzero-agent.bin

RUN chmod +x runzero-agent.bin

# For full functionality the runZero scanner needs to send and receive raw 
# packets, which requires elevated privileges. 
USER root

# The argument `manual` tells runZero not to look for SystemD or upstart.
ENTRYPOINT [ "/opt/runzero/runzero-agent.bin", "manual" ]
