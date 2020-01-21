# Stage 1
FROM mcr.microsoft.com/dotnet/core-nightly/sdk:3.1.101 as build
WORKDIR /app
COPY src/Service2 src/Service2
RUN dotnet build src/Service2

# Stage 2
FROM build as publish
WORKDIR /app
RUN dotnet publish src/Service2 -c Release -o /app -r linux-x64

# Stage 3
FROM mcr.microsoft.com/dotnet/core-nightly/runtime:3.1 AS runtime
WORKDIR /app
COPY --from=publish /app .
CMD dotnet Service2.dll