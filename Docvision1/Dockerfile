FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Docvision1/Docvision1.csproj", "Docvision1/"]
RUN dotnet restore "Docvision1/Docvision1.csproj"
COPY . .
WORKDIR "/src/Docvision1"
RUN dotnet build "Docvision1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Docvision1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Docvision1.dll"]
