#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["publisher/publisher.csproj", "publisher/"]
RUN dotnet restore "publisher/publisher.csproj"
COPY . .
WORKDIR "/src/publisher"
RUN dotnet build "publisher.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "publisher.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "publisher.dll"]