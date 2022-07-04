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
WIP

# https://github.com/quarkusio/quarkus/issues/16225
# https://github.com/quarkusio/quarkus/issues/16225#issuecomment-1172903628

./mvnw package -Pnative -Dquarkus.native.container-build=true -Dquarkus.container-image.build=true

```

https://quarkus.io/guides/building-native-image
> quarkus.native.container-build=true allows for creating a Linux executable without GraalVM being installed (and is only necessary if you don’t have GraalVM installed locally or your local operating system is not Linux)

> quarkus.container-image.build=true instructs Quarkus to create a container-image using the final application artifact (which is the native executable in this case)

### REST

TBD

### gRPC

TBD

### Observability

TBD

### Misc.

- Logging JSON
  - https://quarkus.io/guides/logging#json-logging

## Integration with application/service runtime

### Knative

### Dapr

## Refs.

- https://microprofile.io/
- https://www.graalvm.org/
- https://github.com/graalvm/mandrel