This is a fork, and a branch, off the git tag v13.0.1

We created this fork so we could adjust the SchemaParser to prevent it from checking for a Java enum that matches that of the GraphQL enum.

Initially I did this to create and build the branch:
- sdk install maven (if you don’t have the mvn executable)
- git co v13.0.1 (that’s the version we use now)
- mvn clean install (to build the project)
  - jar is located in ./target/graphql-java-tools-13.0.2-SNAPSHOT.jar
 
I will publish this JAR to our GCP fieler-infra account so we can reference/use it in our fielder-backend build.gradle file.
