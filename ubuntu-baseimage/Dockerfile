FROM ubuntu:20.04

# Prevents installdependencies.sh from prompting the user and blocking the build
ARG DEBIAN_FRONTEND=noninteractive

# Update apt and add docker user
RUN apt update -y && apt upgrade -y && useradd -m docker

# Install Dependencies
RUN apt install -y --no-install-recommends \
    git curl jq build-essential libssl-dev libffi-dev python3 python3-venv python3-dev python3-pip software-properties-common openssh-client wget apt-transport-https curl gnupg unzip vim iputils-ping

# Install Powershell Core
RUN wget -q https://packages.microsoft.com/config/ubuntu/${OS_VERSION}/packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && apt update -y \
    && apt install -y powershell