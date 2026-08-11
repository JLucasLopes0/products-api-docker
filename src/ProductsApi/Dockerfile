# =========================
# STAGE 1 - BUILD
# =========================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia apenas o arquivo do projeto primeiro
COPY ["src/ProductsApi/ProductsApi.csproj", "src/ProductsApi/"]
RUN dotnet restore "src/ProductsApi/ProductsApi.csproj"

# Copia o restante do código
COPY . .
WORKDIR "/app/src/ProductsApi"
RUN dotnet publish -c Release -o /out

# =========================
# STAGE 2 - RUNTIME
# =========================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

COPY --from=build /out .

ENV ASPNETCORE_URLS=http://+:8080

EXPOSE 8080

ENTRYPOINT ["dotnet", "ProductsApi.dll"]
