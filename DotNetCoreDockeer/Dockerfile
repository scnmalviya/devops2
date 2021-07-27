#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
#COPY *.csproj ./
COPY ["DotNetCoreDockeer/DotNetCoreDockeer.csproj", "DotNetCoreDockeer/"]
#USER root
#RUN chmod 755 /src

COPY . .

RUN dotnet restore "DotNetCoreDockeer/DotNetCoreDockeer.csproj"
#COPY . .
WORKDIR "/src/DotNetCoreDockeer"
RUN dotnet build "DotNetCoreDockeer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetCoreDockeer.csproj" -c Release -o /app/publish
#
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetCoreDockeer.dll"]

#COPY . .
#RUN dotnet restore "DockerJenk.csproj"
#WORKDIR "/src/."
#RUN dotnet build "DockerJenk.csproj" --no-restore -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "DockerJenk.csproj" --self-contained false --no-restore -c Release -o /app/publish
#
#RUN dotnet build -c Release
##ENTRYPOINT ["dotnet", "run","--no-launch-profile"]
#ENTRYPOINT ["dotnet", "DockerJenk.dll"]