FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 55095
EXPOSE 44366

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["kafkatest/kafkatest.csproj", "kafkatest/"]
RUN dotnet restore "kafkatest/kafkatest.csproj"
COPY . .
WORKDIR "/src/kafkatest"
RUN dotnet build "kafkatest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "kafkatest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "kafkatest.dll"]