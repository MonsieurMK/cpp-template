FROM debian:bookworm-slim

ARG USERNAME

# --- Installing required packages ---
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    vim \
    git

# --- User management ---
# Create the user and the group
RUN useradd -m -s /bin/bash $USERNAME
# Install sudo and add the user to sudoers
RUN apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
USER $USERNAME
