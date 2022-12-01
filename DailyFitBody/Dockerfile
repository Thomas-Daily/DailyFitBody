FROM mcr.microsoft.com/dotnet/sdk:6.0 AS base
WORKDIR /app
EXPOSE 80/tcp

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DailyFitBody.csproj", "./"]
RUN dotnet restore "DailyFitBody.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DailyFitBody.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DailyFitBody.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DailyFitBody.dll"]
