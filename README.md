# .NET 7 Hello World

En este ejemplo se muestra una pequeña aplicación Hello World .NET Core para [aplicación web de App Service] (https://docs.microsoft.com/azure/app-service-web). Este ejemplo se puede usar en una aplicación .NET Azure App Service, así como en una aplicación Custom Container Azure App Service.

## Ejecutando en un contenedor Docker

Para crear la imagen del contenedor localmente y publicarla localmente, ejecute el siguiente comando:

```docker
docker build -f Dockerfile.linux -t dotnetcore-docs-hello-world-linux . 
docker tag dotnetcore-docs-hello-world-windows <your_registry_name>.azurecr.io/dotnetcore-docs-hello-world-linux:latest
docker push <your_registry_name>.azurecr.io/dotnetcore-docs-hello-world-linux:latest
```