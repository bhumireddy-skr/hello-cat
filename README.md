# Simple Java Web Project (WAR Build)

## How to Build

```sh
mvn clean package
```

The generated WAR file will be available in the `target/` directory.

## How to Deploy

Deploy the WAR file to a servlet container like Apache Tomcat.

## Test

Visit `http://localhost:8080/SimpleJavaWebProject-1.0-SNAPSHOT/hello` after deploying to see the servlet response.