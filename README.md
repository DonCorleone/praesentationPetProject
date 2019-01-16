# Präsentation Suva 22.01.2019

## Server Überblick

### ASP.NET CORE 2.1

- Open Source
- Plattformunabhängig
- C#

#### ASP.NET Core 2.1 mit Angular Starter Template

```bash
dotnet new angular
```

![](_bilder/dotnetNewAngular.png)

project.csproj

```xml
    <PackageReference Include="Microsoft.AspNetCore.App" />
    <PackageReference Include="Microsoft.AspNetCore.Razor.Design" Version="2.1.2" PrivateAssets="All" />
    <PackageReference Include="Microsoft.AspNetCore.SpaServices.Extensions" Version="2.1.1" />
```

_Verworfen weil zu enge Verwebung von Client & Server_

#### ASP.NET WebAPI

```bash
dotnet new webapi
```

![](_bilder/dotnetNewWebapi.png)

project.csproj

```xml
    <PackageReference Include="Microsoft.AspNetCore.App" />
    <PackageReference Include="Microsoft.AspNetCore.Razor.Design" Version="2.1.2" PrivateAssets="All" />
```

## Client Überblick

### Angular (2+)

#### Angular CLI

- Erstellen eines lauffähigen Client

```bash
ng new client
```

- Start des Clients

```bash
./client/ng serve
```

- Start mit Hilfe von node.js

![](_bilder/ngNew.png)

#### NG eject

- Aufhebung der Webpack-Kapselung der Angular CLI

**angular.json**

```json
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "cliStarter": {
      "root": "",
      "sourceRoot": "src",
      "projectType": "application",
      "prefix": "app",
      "schematics": {
        "@schematics/angular:component": {
          "styleext": "scss"
        }
      },
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/cliStarter",
            "index": "src/index.html",
            "main": "src/main.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "src/tsconfig.app.json",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.scss"
            ],
            "scripts": []
          },
```
**bash:**
```bash
ng eject
```

_The 'eject' command has been disabled and will be removed completely in 8.0.
The new configuration format provides increased flexibility to modify the
configuration of your workspace without ejecting._

### Webpack

![](_bilder/webPack.png)

At its core, webpack is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph which maps every module your project needs and generates one or more bundles.

**webpack.dev.js:**

```javascript
const path = require('path');

const webpack = require('webpack');

const HtmlWebpackPlugin = require('html-webpack-plugin');
const CopyWebpackPlugin = require('copy-webpack-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const FilterWarningsPlugin = require('webpack-filter-warnings-plugin');

const helpers = require('./webpack.helpers');

const ROOT = path.resolve(__dirname, '..');

console.log('@@@@@@@@@ USING DEVELOPMENT @@@@@@@@@@@@@@@');
process.traceDeprecation = true;

module.exports = {

    mode: 'development',
    devtool: 'source-map',
    performance: {
        hints: false
    },
    entry: {
        polyfills: './angularApp/polyfills.ts',
        vendor: './angularApp/vendor.ts',
        app: './angularApp/main.ts'
    },
```

**webpack.prod.js:**

```javascript
const path = require('path');

const webpack = require('webpack');

const HtmlWebpackPlugin = require('html-webpack-plugin');
const CopyWebpackPlugin = require('copy-webpack-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const ngToolsWebpack = require('@ngtools/webpack');
const FilterWarningsPlugin = require('webpack-filter-warnings-plugin');
const OfflinePlugin = require('offline-plugin');

const helpers = require('./webpack.helpers');

const ROOT = path.resolve(__dirname, '..');

console.log('@@@@@@@@@ USING PRODUCTION @@@@@@@@@@@@@@@');
process.traceDeprecation = true;

module.exports = {
    mode: 'production',
    entry: {
        vendor: './angularApp/vendor.ts',
        polyfills: './angularApp/polyfills.ts',
        app: './angularApp/main-aot.ts' // AoT compilation
    },

    output: {
        path: ROOT + '/wwwroot/',
        filename: 'dist/[name].[hash].bundle.js',
        chunkFilename: 'dist/[id].[hash].chunk.js',
        publicPath: '/'
    },

    resolve: {
        extensions: ['.ts', '.js', '.json']
    },
```
![](_bilder/webPackUrl.png)

## Datenbanken

### NoSql

- Cosmos DB (Azure)
- Couchbase
- MongoDB

### MongoDB

![](_bilder/MongoDB.png)

- Platzhirsch
- Opensource
- Plattformunabhängig
- JSON
- Javascript-Cli

```javascript
db.inventory.find( { status: { $in: [ "A", "D" ] } } )
```

entspricht im SQL

```sql
SELECT * FROM inventory WHERE status in ("A", "D")
```

- .NET Core Driver

```csharp
//1. Connect to MongoDB instance running on localhost
var client = new MongoClient();

//Access database named 'test'
var database = client.GetDatabase("test");

//Access collection named 'restaurants'
var collection = database.GetCollection("restaurants");
```

- Online University

### SQL

- PostgreSQL
- MySQL
- Azure SQL
- MariaDB

### Maria DB

![](_bilder/MariaDB.png)

- Opensource
- MySql Derrivat
- Plattformunabhängig

## OR-Mapping

- Ausschlaggebender Punkt: Identity on ASP.NET Core als SQL Datenbank
- Entity Framework Core

![](_bilder/efcf.png)

- Code First Ansatz schwierig im NoSQL

![](_bilder/EFCodeFirstVSCode.png)

**Neu generierte Tabellen**

![](_bilder/TabellenSQL.png)

## Hosting

### Varianten

- Azure (Microsoft Cloud)
- Hosting (.NET Core)
- Zu Hause 

### Zu Hause

Webserver mit Datenbanken

![](_bilder/DS216.png)

- Technologieunabhängigkeit
- DevOps Know How
- Linux Know How

## Docker

![](_bilder/docker.png)

- Technologieunabhängigkeit
- Einfachere Installationsroutinen
- Backup Hosting

**docker-compse.yml:**
```yml
version: '3'

services:
  mongodb:
    container_name: mongodbKinderkultur
    image: mongo
    env_file: .env
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_INITDB_ROOT_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_INITDB_ROOT_PASSWORD}
      MONGO_INITDB_DATABASE: ${MONGO_INITDB_DATABASE}
    networks:
      - webapi-network
    ports:
      - "27017:27017"
  maria:
    container_name: mariadbKinderkultur
    image: mariadb
    restart: always
    env_file: .env
    environment:
      MYSQL_ROOT_PASSWORD: ${MARIA_DB_ROOT_PASSWORD}
    networks:
      - webapi-network
    ports:
      - "3306:3306"
networks:
  webapi-network:
    driver: bridge
```

**bash:**
```bash
docker images

REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
backup-mongodb-before-mojave   latest              4499d0d18f33        2 months ago        361MB
backup-mariadb-before-mojave   latest              cd18449acf21        2 months ago        396MB
```

**StartServer-Script:**

```bash
#!/bin/bash
docker start mariadbKinderkultur
docker start mongodbKinderkultur
dotnet run
```


## Demo

### Server

#### Swagger

Tool zum Designen und Testen von RESTful Webservices

```xml
<PackageReference Include="NSwag.AspNetCore" Version="11.17.21" />
```

**Swagger URL:**

![](_bilder/swaggerUrl.png)

**Swagger GET:**

![](_bilder/SwaggerGet.png)

**Swagger Response:**

![](_bilder/SwaggerResponse.png)

#### Versioning

Versionierung der API URL

- Release vs. Production

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Versioning" Version="2.3.0" />
```

#### Source Code

### Client

### Readonly Links

### Anmeldung CMS

### Links Editierbar

### Signal R

