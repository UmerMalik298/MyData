FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_ENVIRONMENT=Development

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["StudentApp/StudentApp.csproj", "./"]
RUN dotnet restore "StudentApp/StudentApp.csproj"
COPY . .
WORKDIR "/src/StudentApp"
RUN dotnet build "StudentApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StudentApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StudentApp.dll"]
