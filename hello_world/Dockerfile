FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
COPY ["hello_world.csproj", "/app"]
RUN dotnet restore "hello_world.csproj"
COPY . .

RUN dotnet build "hello_world.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "hello_world.csproj" -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
EXPOSE 80 443
COPY --from=publish /app/publish/wwwroot .
COPY nginx.conf /etc/nginx/nginx.conf