FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

USER root
ENV DEBIAN_FRONTEND=noninteractive

# Preconfigure the keyboard layout
RUN echo 'keyboard-configuration keyboard-configuration/layoutcode string us' | debconf-set-selections && \
    echo 'keyboard-configuration keyboard-configuration/layout select English (US)' | debconf-set-selections

# Install necessary desktop, VNC, and utility packages cleanly
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        tigervnc-standalone-server \
        xfce4 \
        xfce4-goodies \
        dbus-x11 \
        novnc \
        python3-websockify \
        python3-numpy \
        python3-pip \
        cabextract \
        htop \
        software-properties-common && \
    # Set up Mozilla PPA and correct apt pinning using printf for real newlines
    add-apt-repository -y ppa:mozillateam/ppa && \
    printf "Package: firefox*\nPin: release o=LP-PPA-mozillateam\nPin-Priority: 1001\n" > /etc/apt/preferences.d/Mozilla && \
    apt-get update && \
    apt-get install -y --no-install-recommends firefox && \
    # Clean up apt lists to reduce image size
    rm -rf /var/lib/apt/lists/*
