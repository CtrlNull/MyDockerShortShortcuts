## Dockerize ASP.NET CORE
#### quick reference

Create file > .dockerignore

```bash
$ touch .dockerignore
$ nano .dockerignore
```
add this inside file

```bash
$ node_modules
```
---

Create file > Dockerfile

```bash
$ touch Dockerfile
$ nano Dockerfile
```
add this inside file

```
FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
```

---

#### Build and run Docker image

```bash
$ docker build -t [projectName] .
$ docker run -d -p 8080:80 --name myapp [projectName]
```