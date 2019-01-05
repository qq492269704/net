FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY net/net.csproj net/
RUN dotnet restore net/net.csproj
COPY . .
WORKDIR /src/net
RUN dotnet build net.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish net.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "net.dll"]
