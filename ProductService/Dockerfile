FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ProductService/ProductService.csproj ProductService/
RUN dotnet restore ProductService/ProductService.csproj
COPY ProductService/. ./ProductService/
WORKDIR /src/ProductService
RUN dotnet build ProductService.csproj -c Release -o /app/build
RUN dotnet publish ProductService.csproj -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
COPY ProductService/appsettings.Docker.json ./appsettings.json
ENTRYPOINT ["dotnet", "ProductService.dll"]
