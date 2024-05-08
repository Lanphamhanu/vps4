# Use an official Python runtime as the base image
FROM python:3.9-slim

# Download and extract ngrok
RUN apt-get update && \
    apt-get install -y wget unzip && \
    wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.zip && \
    unzip ngrok-v3-stable-linux-amd64.zip

# Set ngrok authentication token
ENV NGROK_AUTH_TOKEN="2g7quk8KMZh9TzgpeSxH3d8N0KK_2iCyDFFJqydiWzwL6FrVN"

# Install required packages
RUN apt-get update && \
    apt-get install -y net-tools && \
    apt-get install -y procps && \
    apt-get install -y iproute2 && \
    apt-get install -y iputils-ping && \
    apt-get install -y lsof && \
    apt-get install -y openssh-server && \
    apt-get install -y sudo && \
    apt-get clean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* && \
    systemctl enable ssh && \
    systemctl start ssh

# Set up a user for RDP
RUN useradd -m rdpuser && \
    echo "rdpuser:P@ssw0rd!" | chpasswd && \
    adduser rdpuser sudo && \
    echo "rdpuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/rdpuser && \
    service ssh start

# Start ngrok tunnel
CMD ["./ngrok", "tcp", "3389"]
