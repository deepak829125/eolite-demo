FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["eolite-demo.csproj", "."]
RUN dotnet restore "./eolite-demo.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "eolite-demo.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "eolite-demo.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "eolite-demo.dll"]