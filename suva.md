# Präsentation Suva 22.01,2019

## Server

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

## Client

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

```bash
ng eject
```

_The 'eject' command has been disabled and will be removed completely in 8.0.
The new configuration format provides increased flexibility to modify the
configuration of your workspace without ejecting._

