#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Worker.Service/Worker.Service.csproj", "Worker.Service/"]
RUN dotnet restore "Worker.Service/Worker.Service.csproj"
COPY . .
WORKDIR "/src/Worker.Service"
RUN dotnet build "Worker.Service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Worker.Service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Worker.Service.dll"]