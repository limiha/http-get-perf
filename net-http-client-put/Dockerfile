# https://hub.docker.com/_/microsoft-dotnet-core
FROM mcr.microsoft.com/dotnet/core/sdk:3.1.302 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.csproj .
RUN dotnet restore

# copy and publish app and libraries
COPY . .
RUN dotnet publish -c release -o /app --no-restore -f netcoreapp3.1

# final stage/image
FROM mcr.microsoft.com/dotnet/core/runtime:3.1.6
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["./app"]
