#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Marraia.KeyCloak.API/Marraia.KeyCloak.API.csproj", "Marraia.KeyCloak.API/"]
RUN dotnet restore "Marraia.KeyCloak.API/Marraia.KeyCloak.API.csproj"
COPY . .
WORKDIR "/src/Marraia.KeyCloak.API"
RUN dotnet build "Marraia.KeyCloak.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Marraia.KeyCloak.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Marraia.KeyCloak.API.dll"]