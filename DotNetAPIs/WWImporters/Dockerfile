FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["WWImporters/WWImporters.csproj", "WWImporters/"]
RUN dotnet restore "WWImporters/WWImporters.csproj"
COPY . .
WORKDIR "/src/WWImporters"
RUN dotnet build "WWImporters.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WWImporters.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WWImporters.dll"]