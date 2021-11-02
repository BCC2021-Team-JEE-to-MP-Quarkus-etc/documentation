# Brainstorming how to start

Start with the local setup DWP quarkus quick-starter project
[Quarkus.io guide getting-started](https://quarkus.io/guides/getting-started)

| Environment   | JEE  | WF-MP          | Quarkus       |
| ------------- | -----| -------------- | --------------|
| Local DWP     | skip | quick-starter  | quick-starter |
| Local Private | skip | skip           | skip          |
| OpenShift     | skip |                |               |

# Steps

## Use Maven-Wrapper to be shure using Maven 3.8.1
- Install maven 3.8.1 `mvn -N io.takari:maven:wrapper -Dmaven=3.8.1`
- ./mvnw io.quarkus.platform:quarkus-maven-plugin:2.3.1.Final:create -DprojectGroupId=com.baloise -DprojectArtifactId=quarkus-starter -DclassName="com.baloise.codecamp.quarkus.GreetingResource" -Dpath="/hello"
- IntelliJ use mave-wrapper, fix maven-settings.xml override

## Further steps

See Readme [../quarkus-starter/README.md](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/quarkus-starter/blob/main/README.md)

## After building native image via Docker-Container, we're able to build the Dockerimage
```
docker build -t quarkus-starter:dev -f ./src/main/docker/Dockerfile.native-distroless .
docker run --rm -p 8080:8080 -it quarkus-starter:dev
```

## Create GitHub Build Pipeline
GitHub Action to build native quarkus app via docker-container-build, added in [native-build.yml](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/quarkus-starter/blob/main/.github/workflows/native-build.yml)

```
- name: Build with Maven
  run: ./mvnw package -Pnative -Dquarkus.native.container-build=true
```

## Login, Build and Push Image to GitHub Container Registry
Influenced by [using-github-container-registry-in-practice](https:///using-github-container-registry-in-practice-295677c6f65e)
Added in [native-build.yml](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/quarkus-starter/blob/main/.github/workflows/native-build.yml)
```
    - name: Docker login to Container-Registry
      uses: docker/login-action@v1
      with:
        registry: ghcr.io/bcc2021-team-jee-to-mp-quarkus-etc
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}
    - name: Build, Tag & Push Dockerfile
      run: |
        docker build -t ghcr.io/bcc2021-team-jee-to-mp-quarkus-etc/quarkus-starter:${{ GITHUB_SHA }} -f ./src/main/docker/Dockerfile.native-distroless .
        docker push ghcr.io/bcc2021-team-jee-to-mp-quarkus-etc/quarkus-starter:${{ GITHUB_SHA }}
```

### Docker Login

- login-action requires `registry`, `username` and `password`. In the context of the Pipeline, only the registry has to be set explicitly. All other environment-values can be pulled from the GitHub context.
- The registry-name consists of `<registry>/<owner>`. Where '<owner>' should be the organization- or user-name in lowercase letters.

### Docker Build

- We started using native-distroless version ([../quarkus-starter/src/main/docker/Dockerfile.native-distroless](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/quarkus-starter/blob/main/src/main/docker/Dockerfile.native-distroless))

### Docker Push

- The push to the GitHub Container-Registry can be achieved by using standard `docker push` command.  
- The registry-name consists of `<registry>/<owner>/<imagename>`. Where '<owner>' should be the organization- or user-name in lowercase letters.

## Deploy App to the Baloise incubator OKD4-Cluster

Add Application into the `Chart.yaml` and `values.yaml`
See our [OKD4 Deployment Repo](https://github.com/baloise-incubator/code-camp-apps/tree/master/mp-wf-quarkus)

### Test deployed application

[quarkus-quickstart hello path](https://quarkus-starter.apps.okd.baloise.dev/hello)

## Conclusions

- Use Maven-Wrapper for maven 3.8+
- IDE-Support works if maven-wrapper is used
- `quarkus:dev` gives fast dev-cycle feeling!
- javax - Annotations very common compared to classic jee-apps
- Bootable-jar reaches 5.3kb file-size
- Quarkus supports both, generation of uber-jar and also manifest-based runner-jar out of the box
- The running Docker-Container startedwith native-app in 0.018s and consumes 6.4MB memory
- Could be useful in serverless usecases: Fast startup, short living jobs