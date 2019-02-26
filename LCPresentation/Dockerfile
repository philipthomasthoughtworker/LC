FROM microsoft/dotnet-nightly as build-env
WORKDIR /app
COPY . /app

RUN dotnet restore LCPresentation.csproj

RUN apt-get update \
    && apt-get -y install gnupg \
    && curl -sL https://deb.nodesource.com/setup_11.x | bash \
    && apt-get -y install nodejs \
    && apt-get -y install bzip2 \
    && apt-get -y install libfontconfig
    
RUN dotnet publish -c Release -o out

FROM microsoft/dotnet:2.2-aspnetcore-runtime
WORKDIR /app

COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "LCPresentation.dll"]

#docker build .