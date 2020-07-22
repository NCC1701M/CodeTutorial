FROM ubuntu:16.04

# Installing tools
RUN apt-get update \
 && apt-get install -y clang gdb git curl software-properties-common wget

RUN curl -sL https://packagecloud.io/install/repositories/cs50/repo/script.deb.sh | bash -

RUN apt-add-repository -y ppa:cs50/ppa

RUN apt-get install -y libcs50

RUN groupadd --gid 1000 node \
 && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

ENV \
    # Enable detection of running in a container
    DOTNET_RUNNING_IN_CONTAINER=true \
    # Enable correct mode for dotnet watch (only mode supported in a container)
    DOTNET_USE_POLLING_FILE_WATCHER=true \
    # Skip extraction of XML docs - generally not useful within an image/container - helps performance
    NUGET_XMLDOC_MODE=skip

# Set up .Net repository
RUN wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb

RUN dpkg -i packages-microsoft-prod.deb

# Install .Net Core and Entity Framework tools
RUN apt-get update; \
    apt-get install -y apt-transport-https && \
    apt-get update && \
    apt-get install -y dotnet-sdk-3.1 && \
    dotnet help && \
    dotnet tool install --global dotnet-ef
    
# Set up node.js repository
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

# Install node.js
RUN apt-get install -y nodejs

# Install essentials
RUN apt-get install -y build-essential
