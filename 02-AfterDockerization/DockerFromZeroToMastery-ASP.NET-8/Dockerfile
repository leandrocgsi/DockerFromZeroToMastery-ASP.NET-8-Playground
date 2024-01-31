FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
# ENV DOTNET_URLS=http://+:8080
# ENV DOTNET_URLS=https://+:8081
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["DockerFromZeroToMastery-ASP.NET-8/DockerFromZeroToMastery-ASP.NET-8.csproj", "DockerFromZeroToMastery-ASP.NET-8/"]
RUN dotnet restore "./DockerFromZeroToMastery-ASP.NET-8/./DockerFromZeroToMastery-ASP.NET-8.csproj"
COPY . .
WORKDIR "/src/DockerFromZeroToMastery-ASP.NET-8"
RUN dotnet build "./DockerFromZeroToMastery-ASP.NET-8.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./DockerFromZeroToMastery-ASP.NET-8.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerFromZeroToMastery-ASP.NET-8.dll"]