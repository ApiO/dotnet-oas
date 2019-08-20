FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Api.Fu/Api.Fu.csproj", "Api.Fu/"]
RUN dotnet restore "Api.Fu/Api.Fu.csproj"
COPY . .
WORKDIR "/src/Api.Fu"
RUN dotnet build "Api.Fu.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Api.Fu.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Api.Fu.dll"]