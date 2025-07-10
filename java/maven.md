# Apache Maven tips

- [Create a simple project](#create-a-simple-project)

## Create a simple project

```sh
mvn archetype:generate -DgroupId=com.example -DartifactId=sample-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.5 -DinteractiveMode=false
```

- The `-DgroupId` option is used to specify the top level package of your application.
- The `-DartifactId` defines the name of your project and is used as the name of the new folder.

## Run your application

```sh
mvn package && mvn exec:java -Dexec.mainClass="com.example.AppMainClass"
```
