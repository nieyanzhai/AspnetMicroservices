FROM mcr.microsoft.com/dotnet/aspnet:5.0-focal AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:5.0-focal AS build
WORKDIR /src
COPY ["src/ApiGateway/OcelotApiGateway/OcelotApiGateway.csproj", "src/ApiGateway/OcelotApiGateway/"]
RUN dotnet restore "src/ApiGateway/OcelotApiGateway/OcelotApiGateway.csproj"
COPY . .
WORKDIR "/src/src/ApiGateway/OcelotApiGateway"
RUN dotnet build "OcelotApiGateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OcelotApiGateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OcelotApiGateway.dll"]
