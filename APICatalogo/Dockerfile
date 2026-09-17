FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copia o .csproj diretamente da pasta atual
COPY ["APICatalogo.csproj", "./"]
RUN dotnet restore "APICatalogo.csproj"

# Copia todos os arquivos da pasta atual
COPY . .
RUN dotnet build "APICatalogo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "APICatalogo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
ENV ASPNETCORE_ENVIRONMENT=Development
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "APICatalogo.dll"]
