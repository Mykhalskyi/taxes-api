FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["TaxesApi/TaxesApi.csproj", "TaxesApi/"]
RUN dotnet restore "TaxesApi/TaxesApi.csproj"
COPY . .
WORKDIR "/src/TaxesApi"
RUN dotnet build "TaxesApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TaxesApi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TaxesApi.dll"]
