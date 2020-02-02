FROM mcr.microsoft.com/dotnet/core/sdk:3.1 as build
WORKDIR /src
COPY NPWD.csproj .
RUN dotnet restore NPWD.csproj
COPY . .
RUN dotnet build NPWD.csproj -c Release -o app/build
FROM build as publish
RUN dotnet publish NPWD.csproj -c Release -o app/publish
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=publish /src/app/publish .
ENTRYPOINT ["dotnet", "NPWD.dll"]