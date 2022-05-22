#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LMS_Author_Api/LMS_Author_Api.csproj", "LMS_Author_Api/"]
RUN dotnet restore "LMS_Author_Api/LMS_Author_Api.csproj"
COPY . .
WORKDIR "/src/LMS_Author_Api"
RUN dotnet build "LMS_Author_Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LMS_Author_Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LMS_Author_Api.dll"]