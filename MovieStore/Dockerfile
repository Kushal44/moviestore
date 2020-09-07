FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["MovieStore/MovieStore.csproj", "MovieStore/"]
RUN dotnet restore "MovieStore/MovieStore.csproj"
COPY . .
WORKDIR "/src/MovieStore"
RUN dotnet build "MovieStore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MovieStore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MovieStore.dll"]
