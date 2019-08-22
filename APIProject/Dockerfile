FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["APIProject/APIProject.csproj", "APIProject/"]
RUN dotnet restore "APIProject/APIProject.csproj"
COPY . .
WORKDIR "/src/APIProject"
RUN dotnet build "APIProject.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "APIProject.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "APIProject.dll"]