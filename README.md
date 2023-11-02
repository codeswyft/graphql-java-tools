This is a fork, and a branch, off the git tag v13.0.1

We created this fork so we could adjust the SchemaParser to prevent it from checking for a Java enum that matches that
of the GraphQL enum.

Initially I did this to create and build the branch:

- sdk install maven (if you don’t have the mvn executable)
- git co v13.0.1 (that’s the version we use now)
- mvn clean install (to build the project)
    - jar is located in ./target/graphql-java-tools-13.0.2-SNAPSHOT.jar

## Publishing (Maven)

To publish this JAR to our GCP `fiedler-infra` account simply run this (it will build and deploy/push it to GCP):

```
mvn deploy
```

NOTE: To publish the JAR you will need create the file `~/.m2/settings.xml`. See `fielder-infra` security manager for
the secret `M2_SETTINGS_XML_FILE` that has the contents of the file you
need.

## Using the JAR (Gradle)

```
repositories {
    mavenLocal()
    maven {
        url "https://us-central1-maven.pkg.dev/fielder-infra/fielder-central"
        credentials {
            username = "_json_key_base64"
            password = System.getenv('FIELDER_CENTRAL_PWD')
        }
        authentication {
            basic(BasicAuthentication)
        }
    }
    mavenCentral()
    google()
}
```

And (match whatever version you want to pull):

```
implementation 'com.graphql-java-kickstart:graphql-java-tools:13.0.5'
```

NOTE: To access the JAR you will need create an env var `FIELDER_CENTRAL_PWD`. See `fielder-infra` security manager for
the secret `FIELDER_CENTRAL_PWD` that you should use to set your env var (in your `~/.zshrc` file).

## Local Development

To publish this JAR to your local maven repo:

```
mvn install:install-file -Dfile=target/graphql-java-tools-13.0.4.jar -DgroupId=com.graphql-java-kickstart -DartifactId=graphql-java-tools -Dversion=13.0.4 -Dpackaging=jar
```

To use this JAR as a dependency in your gradle project, adjust your build.gradle as follows:

```
repositories {
    mavenLocal() // << add that if you want to build locally and use it
    mavenCentral()
    google()
}
```

And (match whatever version is defined in the `pom.xml` file):

```
implementation 'com.graphql-java-kickstart:graphql-java-tools:13.0.4'
```
