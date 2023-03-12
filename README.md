## Overaching recomendation and explanation

Docker compose simply and quickly builds local container constelations. As a such it has to be very carefuly used on company laptops. Where the "other contaners" are company property and might be overexposed if pulled to dev's laptops.

This demo uses Azure SQL EDGE, [an IoT version of Azure SQL engine](https://github.com/docker/awesome-compose/tree/master/aspnet-mssql).

This Compose.yaml can be easily changed so that it uses [Microsoft SQL Server - Ubuntu based images](https://hub.docker.com/_/microsoft-mssql-server). See the "How to use ... section.

>
> NOTE: none of this is secure for company prod environments. 
> 
"The only way" is to test only online and use Azure Key Vault with a secret "master key" known only at production run-time. And then programaticaly start the required on-line parts. Or have them available like Azure SQL DB's.

 Ultimately no local container constelations should be composed on dev's laptops. All the testing should be done on the online DEVENV.

 In some cases local development might be done with mockup data, fake passwords and such. Using well known public domain container, like MS SQL SRV official containers and such.

<h3>&nbsp;</h3>

---

<h3>&nbsp;</h3>

# Docker Compose sample application
# [ASP.NET with MS SQL server database](https://github.com/docker/awesome-compose/tree/master/aspnet-mssql)

Project structure:
```
.
├── app
│   ├── aspnetapp
│   │   ├── appsettings.Development.json
|   |   └── ...
│   ├── ...
│   └── Dockerfile
└── compose.yaml
```

[_compose.yaml_](compose.yaml)
```
services:
  web:
    build: app
    ports:
    - 80:80
  db:
    # mssql server image isn't available for arm64 architecture, so we use azure-sql instead
    image: mcr.microsoft.com/azure-sql-edge:1.0.4
    # If you really want to use MS SQL Server, uncomment the following line
    #image: mcr.microsoft.com/mssql/server
    ...
```
The compose file defines an application with two services `web` and `db`. The image for the web service is built with the Dockerfile inside the `app` directory (build parameter).

When deploying the application, docker compose maps the container port 80 to port 80 of the host as specified in the file.
Make sure port 80 on the host is not being used by another container, otherwise the port should be changed.

> ℹ️ **_INFO_**  
> For compatibility purpose between `AMD64` and `ARM64` architecture, we use Azure SQL Edge as database instead of MS SQL Server.  
> You still can use the MS SQL Server image by uncommenting the following line in the Compose file   
> `#image: mcr.microsoft.com/mssql/server`

## Deploy with docker compose

```
$ docker compose up -d
Creating network "aspnet-mssql_default" with the default driver
Building web
Step 1/13 : FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
2.1: Pulling from dotnet/core/sdk
....
....
a9dca2f6722a: Pull complete
Digest: sha256:9b700672670bb3db4b212e8aef841ca79eb2fce7d5975a5ce35b7129a9b90ec0
Status: Downloaded newer image for microsoft/mssql-server-linux:latest
Creating aspnet-mssql_web_1 ... done
Creating aspnet-mssql_db_1  ... done
```


## Expected result

Listing containers must show two containers running and the port mapping as below:
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
7f3a2a7ea5c0        microsoft/mssql-server-linux   "/opt/mssql/bin/sqls…"   4 minutes ago       Up 4 minutes        1433/tcp             aspnet-mssql_db_1
27342dde8b64        aspnet-mssql_web               "dotnet aspnetapp.dll"   4 minutes ago       Up 4 minutes        0.0.0.0:80->80/tcp   aspnet-mssql_web_1
```

After the application starts, navigate to `http://localhost:80` in your web browser.

![page](media/output.jpg)

Stop and remove the containers

```
$ docker compose down
```
