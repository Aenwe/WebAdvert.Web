FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["WebAdvert.Web.csproj", ""]
RUN dotnet restore "./WebAdvert.Web.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WebAdvert.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebAdvert.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebAdvert.Web.dll"]