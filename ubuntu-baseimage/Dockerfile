FROM ubuntu:20.04

# Set the Arguments for the Dockerfile
ARG RUNNER_VERSION="2.314.1"        # Use this to set the Download Version for the Runner
ARG OS_VERSION="20.04"              # Use this to set the Download Version for the Microsoft Repo

# Set Envirorment Variables based on the Arguements
ENV RUNNER_VERSION=${RUNNER_VERSION}
ENV OS_VERSION=${OS_VERSION}

# Prevents installdependencies.sh from prompting the user and blocking the image creation
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