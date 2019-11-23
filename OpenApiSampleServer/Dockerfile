FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["OpenApiSampleServer/OpenApiSampleServer.csproj", "OpenApiSampleServer/"]
RUN dotnet restore "OpenApiSampleServer/OpenApiSampleServer.csproj"
COPY . .
WORKDIR "/src/OpenApiSampleServer"
RUN dotnet build "OpenApiSampleServer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OpenApiSampleServer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OpenApiSampleServer.dll"]