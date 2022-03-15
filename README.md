# azure-spring-cloud-helloworld

See [Azure Spring Cloud](https://docs.microsoft.com/en-us/azure/spring-cloud/quickstart?tabs=Azure-CLI&pivots=programming-language-java)

[Start with Spring Initializr](https://start.spring.io/#!type=maven-project&language=java&platformVersion=2.6.4&packaging=jar&jvmVersion=11&groupId=com.example&artifactId=hellospring&name=hellospring&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.hellospring&dependencies=web,cloud-eureka,actuator,cloud-config-client)

Select Generate when all the dependencies are set.

Download and unpack the package, then create a web controller for a simple web application by adding the file src/main/java/com/example/hellospring/HelloController.java with the following contents:

```sh
package com.example.hellospring;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
public class HelloController {

    @RequestMapping("/")
    public String index() {
        return "Greetings from Azure Spring Cloud!";
    }

}
```


Build the project using Maven:
```sh
mvn clean package -DskipTests
```

# With Public endpoint
Create the app with a public endpoint assigned.
```sh
az spring-cloud app create -n hellospring -s <service instance name> -g <resource group name> --assign-endpoint true --runtime-version=Java_11
```

Deploy the Jar file for the app (target\hellospring-0.0.1-SNAPSHOT.jar on Windows):
```sh
az spring-cloud app deploy -n hellospring -s <service instance name> -g <resource group name> --artifact-path azure-spring-cloud-helloworld/target/hellospring-0.0.1-SNAPSHOT.jar
```

Once deployment has completed, you can access the app at https://<service instance name>-hellospring.azuremicroservices.io/.

Use the following command to get real-time logs from the App.
```sh
az spring-cloud app logs -n hellospring -s <service instance name> -g <resource group name> --lines 100 -f
```

# Without Public endpoint
Create the app with a public endpoint assigned.
```sh
az spring-cloud app create -n hellonopub -s <service instance name> -g <resource group name> --assign-endpoint false --runtime-version=Java_11
```

Deploy the Jar file for the app (target\hellospring-0.0.1-SNAPSHOT.jar on Windows):
```sh
az spring-cloud app deploy -n hellonopub -s <service instance name> -g <resource group name> --artifact-path azure-spring-cloud-helloworld/target/hellospring-0.0.1-SNAPSHOT.jar
```

Once deployment has completed, you can access the app at https://<service instance name>-hellospring.azuremicroservices.io/.

Use the following command to get real-time logs from the App.
```sh
az spring-cloud app logs -n hellonopub -s <service instance name> -g <resource group name> --lines 100 -f
```


# Cleanup
```sh
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az group delete --name $resourceGroupName &&
echo "Press [ENTER] to continue ..."
```

# Issues
- [https://github.com/MicrosoftDocs/azure-docs/issues/89797](https://github.com/MicrosoftDocs/azure-docs/issues/89797)
- [https://github.com/MicrosoftDocs/azure-docs/issues/89796](https://github.com/MicrosoftDocs/azure-docs/issues/89796)
- [https://github.com/microsoft/CBL-Mariner/issues/2484](https://github.com/microsoft/CBL-Mariner/issues/2484)
- [https://github.com/actions/runner/issues/1750](https://github.com/actions/runner/issues/1750)