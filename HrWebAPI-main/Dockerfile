FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env

ENV ASPNETCORE_ENVIRONMENT=Development
EXPOSE 5085
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "HRWebAPI.dll"]

#FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
#WORKDIR /app
#EXPOSE 5085
#
## Build stage
#FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
#WORKDIR /src
#COPY ["HrWebAPI-main/HrWebAPI.csproj", "HrWebAPI/"]
#RUN dotnet restore "HrWebAPI-main/HrWebAPI.csproj"
#COPY . .
#WORKDIR "/src/HrWebAPI"
#RUN dotnet build "HrWebAPI.csproj" -c Release -o /app/build
#
## Publish stage
#FROM build AS publish
#RUN dotnet publish "HrWebAPI.csproj" -c Release -o /app/publish
#
## Final stage
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "HrWebAPI.dll"]