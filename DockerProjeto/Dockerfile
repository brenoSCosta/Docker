FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["DockerProjeto.csproj", ""]
RUN dotnet restore "./DockerProjeto.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DockerProjeto.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerProjeto.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerProjeto.dll"]