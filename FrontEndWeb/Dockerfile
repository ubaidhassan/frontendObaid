FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["FrontEndWeb/FrontEndWeb.csproj", "FrontEndWeb/"]
RUN dotnet restore "FrontEndWeb/FrontEndWeb.csproj"
COPY . .
WORKDIR "/src/FrontEndWeb"
RUN dotnet build "FrontEndWeb.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "FrontEndWeb.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FrontEndWeb.dll"]