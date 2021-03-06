#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["api01/api01.csproj", "api01/"]
RUN dotnet restore "api01/api01.csproj"
COPY . .
WORKDIR "/src/api01"
RUN dotnet build "api01.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "api01.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "api01.dll"]