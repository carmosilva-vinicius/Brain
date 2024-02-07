[Docker](https://roadmap.sh/docker) is an open-source platform that automates the deployment, scaling, and management of applications by isolating them into lightweight, portable containers. [[Container|Containers]] are standalone executable units that encapsulate all necessary dependencies, libraries, and configuration files required for an application to run consistently across various environments.

## Build
- **-t** or **--tag** : Set the name and optionally a tag (format: "name:tag")
- **.** : Path to Docker file
```sh
docker build -t api-proxy .
```

## Run
```sh
docker run -d -p 8080:80 --name api-proxy --rm api-proxy
```