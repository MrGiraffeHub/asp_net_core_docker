#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["SecondWeb.API/SecondWeb.API.csproj", "SecondWeb.API/"]
RUN dotnet restore "SecondWeb.API/SecondWeb.API.csproj"
COPY . .
WORKDIR "/src/SecondWeb.API"
RUN dotnet build "SecondWeb.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SecondWeb.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SecondWeb.API.dll"]