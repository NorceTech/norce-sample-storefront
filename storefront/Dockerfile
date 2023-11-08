FROM mcr.microsoft.com/dotnet/aspnet:7.0-bookworm-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src
COPY ["storefront/Storefront.csproj", "storefront/"]
RUN dotnet restore "storefront/Storefront.csproj"
COPY . .
WORKDIR "/src/storefront"
RUN dotnet build "Storefront.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Storefront.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

ENV TZ=Europe/Stockholm
ENV ASPNETCORE_URLS=http://+:1800

ENTRYPOINT ["dotnet", "Storefront.dll"]