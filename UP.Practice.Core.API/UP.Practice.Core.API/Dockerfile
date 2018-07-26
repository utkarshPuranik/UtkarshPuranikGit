FROM microsoft/aspnetcore:2.0-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-sac2016 AS build
WORKDIR /src
COPY *.sln ./
COPY UP.Practice.Core.API/UP.Practice.Core.API.csproj UP.Practice.Core.API/
RUN dotnet restore
COPY . .
WORKDIR /src/UP.Practice.Core.API
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "UP.Practice.Core.API.dll"]
