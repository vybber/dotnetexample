FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["helloworld/helloworld.csproj", "helloworld/"]

RUN dotnet restore "helloworld/helloworld.csproj"
COPY . .
WORKDIR "/src/helloworld"
RUN dotnet build "helloworld.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "helloworld.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "helloworld.dll"]