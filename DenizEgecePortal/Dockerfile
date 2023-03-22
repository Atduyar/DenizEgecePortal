FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DenizEgecePortal/DenizEgecePortal.csproj", "DenizEgecePortal/"]
RUN dotnet restore "DenizEgecePortal/DenizEgecePortal.csproj"
COPY . .
WORKDIR "/src/DenizEgecePortal"
RUN dotnet build "DenizEgecePortal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DenizEgecePortal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DenizEgecePortal.dll"]
