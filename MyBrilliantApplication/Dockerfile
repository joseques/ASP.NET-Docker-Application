FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY MyBrilliantApplication/MyBrilliantApplication.csproj MyBrilliantApplication/
RUN dotnet restore MyBrilliantApplication/MyBrilliantApplication.csproj
COPY . .
WORKDIR /src/MyBrilliantApplication
RUN dotnet build MyBrilliantApplication.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish MyBrilliantApplication.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyBrilliantApplication.dll"]