FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["AuthenticationAuthorization/AuthenticationAuthorization.csproj", "AuthenticationAuthorization/"]
RUN dotnet restore "AuthenticationAuthorization/AuthenticationAuthorization.csproj"
COPY . .
WORKDIR "/src/AuthenticationAuthorization"
RUN dotnet build "AuthenticationAuthorization.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AuthenticationAuthorization.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AuthenticationAuthorization.dll"]