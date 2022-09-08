FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MyFirstWebApi/MyFirstWebApi.csproj", "MyFirstWebApi/"]
RUN dotnet restore "MyFirstWebApi/MyFirstWebApi.csproj"
COPY . .
WORKDIR "/src/MyFirstWebApi"
RUN dotnet build "MyFirstWebApi.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "MyFirstWebApi.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyFirstWebApi.dll"]