#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CleanArchitecture.WebUI/CleanArchitecture.WebUI.csproj", "CleanArchitecture.WebUI/"]
RUN dotnet restore "CleanArchitecture.WebUI/CleanArchitecture.WebUI.csproj"
COPY . .
WORKDIR "/src/CleanArchitecture.WebUI"
RUN dotnet build "CleanArchitecture.WebUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CleanArchitecture.WebUI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CleanArchitecture.WebUI.dll"]