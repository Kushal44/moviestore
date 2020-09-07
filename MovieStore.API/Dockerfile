FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["MovieStore.API/MovieStore.API.csproj", "MovieStore.API/"]
RUN dotnet restore "MovieStore.API/MovieStore.API.csproj"
COPY . .
WORKDIR "/src/MovieStore.API"
RUN dotnet build "MovieStore.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MovieStore.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MovieStore.API.dll"]
