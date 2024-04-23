# .NET 7 Hello World

En este ejemplo se muestra una pequeña aplicación Hello World .NET Core para [aplicación web de App Service] (https://docs.microsoft.com/azure/app-service-web). Este ejemplo se puede usar en una aplicación .NET Azure App Service, así como en una aplicación Custom Container Azure App Service.

## Creando archivo Dockerfile

En la raíz del proyecto crear el archivo Dockerfile y colocar los siguientes comandos:

```
# Start with the .NET SDK for building the app
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
# Work within a folder named `/source`
WORKDIR /source

# Copy everything in this project and build app
COPY . ./dotnetcore-docs-hello-world/
WORKDIR /source/dotnetcore-docs-hello-world
RUN dotnet publish -c release -o /app 

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /app ./

# Expose port 80
# This is important in order for the Azure App Service to pick up the app
ENV PORT 80
EXPOSE 80

# Start the app
ENTRYPOINT ["dotnet", "dotnetcoresample.dll"]

```

## Ejecutando en un contenedor Docker

Para crear la imagen del contenedor localmente y publicarla localmente, ejecute el siguiente comando:

```docker
docker build -f Dockerfile -t simple-dotnet-fronted . 
docker tag simple-dotnet-fronted <your_registry_name>.azurecr.io/dotnetcore-docs-hello-world-linux:latest
docker push <your_registry_name>.azurecr.io/dotnetcore-docs-hello-world-linux:latest
```