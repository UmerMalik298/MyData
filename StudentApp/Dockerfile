# Base image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_ENVIRONMENT=Development

# Build image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["StudentApp/StudentApp.csproj", "StudentApp/"]

RUN dotnet restore "StudentApp.csproj"
COPY StudentApp/ ./StudentApp/
WORKDIR "/src/StudentApp"
RUN dotnet build "StudentApp.csproj" -c Release -o /app/build

# Publish
FROM build AS publish
RUN dotnet publish "StudentApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Final image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StudentApp.dll"]
