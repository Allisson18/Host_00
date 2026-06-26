FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
# Altera a cópia para buscar de dentro da pasta Hospedagem00
COPY ["Hospedagem00/Hospedagem00.csproj", "Hospedagem00/"]
RUN dotnet restore "Hospedagem00/Hospedagem00.csproj"
COPY . .
WORKDIR "/src/Hospedagem00"
RUN dotnet build "Hospedagem00.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hospedagem00.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hospedagem00.dll"]