FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt install -y nodejs
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
RUN export NVM_DIR="$HOME/.nvm"
