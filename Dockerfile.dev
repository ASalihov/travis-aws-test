FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src

COPY test-containerized-web-app.sln .
COPY ./test-containerized-web-app ./test-containerized-web-app
COPY ./tests ./tests

RUN dotnet restore test-containerized-web-app.sln
RUN dotnet publish test-containerized-web-app/test-containerized-web-app.csproj -c Release -o /app
RUN dotnet publish tests/tests.csproj -c Release -o /app/tests
COPY ./resources/text.txt ./app/resources

FROM base AS final
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "test-containerized-web-app.dll"]


