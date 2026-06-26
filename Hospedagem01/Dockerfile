FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
# Usando o nome do seu novo projeto: Hospedagem01
COPY ["Hospedagem01/Hospedagem01.csproj", "Hospedagem01/"]
RUN dotnet restore "Hospedagem01/Hospedagem01.csproj"
COPY . .
WORKDIR "/src/Hospedagem01"
RUN dotnet build "Hospedagem01.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hospedagem01.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hospedagem01.dll"]