FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DockerApps.BlazorFrontend/DockerApps.BlazorFrontend.csproj", "DockerApps.BlazorFrontend/"]
RUN dotnet restore "DockerApps.BlazorFrontend/DockerApps.BlazorFrontend.csproj"
COPY . .
WORKDIR "/src/DockerApps.BlazorFrontend"
RUN dotnet build "DockerApps.BlazorFrontend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerApps.BlazorFrontend.csproj" -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY DockerApps.BlazorFrontend/nginx.conf /etc/nginx/nginx.conf