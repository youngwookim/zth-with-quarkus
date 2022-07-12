# zth-with-quarkus
Zero to Hero with Quarkus

## Quarks?

https://quarkus.io/
> Quarkus was created to enable Java developers to create applications for a modern, cloud-native world. Quarkus is a Kubernetes-native Java framework tailored for GraalVM and HotSpot, crafted from best-of-breed Java libraries and standards. The goal is to make Java the leading platform in Kubernetes and serverless environments while offering developers a framework to address a wider range of distributed application architectures.


## Quickstart

Prerequisites:
- JDK 17
- sdkman

```
# via quarkus cli

$ sdk install quarkus
$ quarkus version
2.10.0.Final

$ quarkus create && cd code-with-quarkus
$ ./mvn compile quarkus:dev

$ curl -X GET http://localhost:8080/hello
Hello from RESTEasy Reactive

```

Browse http://localhost:8080/q/dev/ for Dev UI (on dev env.)

Configure your quarkus app.:
- https://code.quarkus.io/

## Developing Quarkus Applications

- https://quarkus.io/guides/
- https://github.com/quarkusio/quarkus-quickstarts
- https://github.com/quarkusio/quarkus-super-heroes


## Local development with Rancher Desktop

Prerequisites:
- Rancher Desktop (k3s)
- Docker Compose
- Quarkus Extentions
  - Jib
  - Kubernetes

```
# https://quarkus.io/guides/container-image#container-image-options

$ ./mvnw clean package -Dquarkus.container-image.build=true -Dquarkus.kubernetes.image-pull-policy=Never

(snip)
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Created container image 1110551/code-with-quarkus:1.0.0-SNAPSHOT (sha256:ec4d12f922615bdd21a424b5f59872465fc862b04ce47d3215f6dfd8b8e14e64)

# docker-compose
TBD

# Kubernetes
$ kubectl apply -f target/kubernetes/kubernetes.yml 
$ kubectl get po

```

## Native excutable & container

WIP

- https://quarkus.io/guides/building-native-image
- https://quarkus.io/guides/building-native-image#creating-a-container

Native excutable:
```
# install graalvm via sdkman

$ sdk list java
$ sdk install java [id]

$ export GRAALVM_HOME=$HOME/.sdkman/candidates/java/[id]/
$ $GRAALVM_HOME/bin/gu install native-image
......
$ mvn clean package -Pnative

$ ./target/code-with-quarkus-1.0.0-SNAPSHOT-runner

```

Container:
```

# x86
$ ./mvnw clean install -Pnative -Dquarkus.native.container-build=true -Dquarkus.container-image.build=true
$ docker run -i --rm -p 8080:8080 1110551/code-with-quarkus:1.0.0-SNAPSHOT

# Apple M1
$ ./mvnw clean install -Pnative -DskipTests -Dquarkus.native.container-build=true -Dquarkus.container-image.build=true -Dquarkus.native.builder-image=quay.io/quarkus/ubi-quarkus-mandrel:22.1-java17-arm64 -Dquarkus.native.native-image-xmx=8g

# https://github.com/quarkusio/quarkus/issues/16225
# https://github.com/quarkusio/quarkus/issues/16225#issuecomment-1172903628
# https://github.com/quarkusio/quarkus/issues/16225#issuecomment-999549585

```

https://quarkus.io/guides/building-native-image
> quarkus.native.container-build=true allows for creating a Linux executable without GraalVM being installed (and is only necessary if you don’t have GraalVM installed locally or your local operating system is not Linux)

> quarkus.container-image.build=true instructs Quarkus to create a container-image using the final application artifact (which is the native executable in this case)

### HTTP / REST


REST Client (Reactive):
- https://quarkus.io/guides/rest-client-reactive

```
quarkus ext add io.quarkus:quarkus-resteasy-reactive
quarkus ext add io.quarkus:quarkus-smallrye-openapi
quarkus ext add io.quarkus:quarkus-container-image-jib
quarkus ext add io.quarkus:quarkus-kubernetes
quarkus ext add io.quarkus:quarkus-smallrye-health
quarkus ext add io.quarkus:quarkus-micrometer
quarkus ext add io.quarkus:quarkus-micrometer-registry-prometheus
quarkus ext add io.quarkus:quarkus-logging-json
quarkus ext add io.quarkiverse.microprofile:quarkus-microprofile
```

### gRPC

```
quarkus ext add io.quarkus:quarkus-grpc
quarkus ext add io.quarkus:quarkus-container-image-jib
quarkus ext add io.quarkus:quarkus-kubernetes
quarkus ext add io.quarkus:quarkus-smallrye-health
quarkus ext add io.quarkus:quarkus-micrometer
quarkus ext add io.quarkus:quarkus-micrometer-registry-prometheus
quarkus ext add io.quarkus:quarkus-logging-json
quarkus ext add io.quarkiverse.microprofile:quarkus-microprofile
```

# Kubernetes

k3s:
  - https://stackoverflow.com/questions/68761409/jcapemkeyconverter-is-provided-by-bouncycastle-an-optional-dependency-to-use-s/72872000#72872000

### Observability

TBD

### Misc.

- Logging JSON
  - https://quarkus.io/guides/logging#json-logging

## Integration with application/service runtime

### Knative

- https://knative.dev/
- https://github.com/quarkusio/quarkus-quickstarts/tree/main/getting-started-knative
- https://medium.com/@roudranil/quarkus-a-quickstart-459ecb62ca1f
- https://quarkus.io/guides/funqy-knative-events
- https://github.com/quarkusio/quarkus-quickstarts/tree/main/funqy-quickstarts/funqy-knative-events-quickstart

### Dapr

TBD

## Refs.

- https://microprofile.io/
- https://www.graalvm.org/
- https://github.com/graalvm/mandrel
- https://www.youtube.com/watch?v=8age_72M_NE&t=1219s