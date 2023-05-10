FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["HundredPointTaskScoring/HundredPointTaskScoring.csproj", "HundredPointTaskScoring/"]
RUN dotnet restore "HundredPointTaskScoring/HundredPointTaskScoring.csproj"
COPY . .
WORKDIR "/src/HundredPointTaskScoring"
RUN dotnet build "HundredPointTaskScoring.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HundredPointTaskScoring.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HundredPointTaskScoring.dll"]
