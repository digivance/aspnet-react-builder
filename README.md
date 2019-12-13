# ASP.Net Core & React
aspnet-react-builder is an open source docker image that developers can use to easily compile ASP.Net core web applications using React as their front end. Specifically, with this image you can run dotnet build on a project build from the standard Visual Studio ASP.Net web application with react template.

## Simple Use Case
A simple use case, you have created a small demo project and want to build your application as a docker image containing all of the .NET Core, Npm and NodeJS frameworks and tools. You might do this for your beta testing machine so that you can shell into it and use the development tools to test out fixes to bugs. To do this, create a Dockerfile in the project root (where the .csproj file is) containing the following:

````
FROM digivance/aspnet-react-builder:3.1 AS builder
WORKDIR /src
COPY . .

RUN dotnet publish "<your-project>.csproj" -c Release -o /app/publish
````

## General Use Case
It is a good practice to host your application from a fresh production image rather than from the image used to build your application. This ensures none of the development tools (or their overhead) are installed on your production application. To do this, create a Dockerfile in the project root (where the .csproj file is) containing the following: (note we are using buster-slim, a trimmed down version of Debian buster)

````
FROM digivance/aspnet-react-builder:3.1 AS build
WORKDIR /src
COPY . .
RUN dotnet publish "<your-project>.csproj" -c Release -o /app

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim
WORKDIR /app
COPY --from=build /app .

EXPOSE 80
EXPOSE 443
ENTRYPOINT ["dotnet", "<your-project>.dll"]
````

## Support
Please submit any bugs or feature requests as issues here on github, we're happy to help! Digivance develops and maintains open source projects and cloud service offerings for developers, please see our website to learn more about what we offer and or to contact our team.

www.Digivance.com
