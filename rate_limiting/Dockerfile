FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["rate_limiting/rate_limiting.csproj", "rate_limiting/"]
RUN dotnet restore "rate_limiting/rate_limiting.csproj"
COPY . .
WORKDIR "/src/rate_limiting"
RUN dotnet build "rate_limiting.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "rate_limiting.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "rate_limiting.dll"]