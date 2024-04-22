FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt update && \
    apt upgrade -y;

RUN apt install build-essential \
                procps \
                curl \
                file \
                git \
                -y -q --allow-unauthenticated;
RUN rm -rf /var/lib/apt/lists/*

RUN useradd -m -s /bin/zsh linuxbrew && \
    usermod -aG sudo linuxbrew &&  \
    mkdir -p /home/linuxbrew/.linuxbrew && \
    chown -R linuxbrew: /home/linuxbrew/.linuxbrew

USER linuxbrew
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

USER root
RUN chown -R $CONTAINER_USER: /home/linuxbrew/.linuxbrew
ENV PATH="/home/linuxbrew/.linuxbrew/bin:${PATH}"
RUN git config --global --add safe.directory /home/linuxbrew/.linuxbrew/Homebrew; \
    brew update; \
    brew doctor;

RUN brew install gcc python@3.12 pipx;
RUN pipx install poetry; \
    pipx ensurepath --force;
