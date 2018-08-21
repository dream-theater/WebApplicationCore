FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY WebApplicationCore/WebApplicationCore.csproj WebApplicationCore/
RUN dotnet restore WebApplicationCore/WebApplicationCore.csproj
COPY . .
WORKDIR /src/WebApplicationCore
RUN dotnet build WebApplicationCore.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplicationCore.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplicationCore.dll"]
