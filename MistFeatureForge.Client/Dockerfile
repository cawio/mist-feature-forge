FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

COPY ["MistFeatureForge.Client.csproj", "./"]
RUN dotnet restore "MistFeatureForge.Client.csproj"

COPY . .
RUN dotnet build "MistFeatureForge.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MistFeatureForge.Client.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
EXPOSE 8080

ENTRYPOINT ["dotnet", "MistFeatureForge.Client.dll"]