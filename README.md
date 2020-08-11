# Monitor de APIs

## Monitor

É necessário que a aplicação do monitor tenham a dependência a seguir no `pom.xlm`.

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-server</artifactId>
    <version>{version}</version>
</dependency>
```

Já na classe principal:

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.context.annotation.Configuration;

import de.codecentric.boot.admin.server.config.EnableAdminServer;

@Configuration
@EnableAutoConfiguration
@EnableAdminServer
public class MonitoramentoApplication {

    public static void main(String[] args) {
        SpringApplication.run(MonitoramentoApplication.class, args);
    }

}
```

**OBS:** O monitor deve rodar em uma porta dedicada para ele.

----------

## Cliente

Já para o(s) cliente(s) é necssária adicionar as dependências do Actuator e Spring Boot Admin Starter Client.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.2.3</version>
</dependency>
```

As demais configurações estarão no arquivo de propriedades.

### **application.properties**

```properties
# actuator
management.endpoint.health.show-details=always
management.endpoints.web.exposure.include=*
info.app.name=@project.name@
info.app.description=@project.description@
info.app.version=@project.version@
info.app.encoding=@project.build.sourceEncoding@
info.app.java.version=@java.version@

# spring boot admin server
spring.boot.admin.client.url=http://localhost:8081

```

### **application.yml**

```yml
# actuator
info:
    app:
        description: '@project.description@'
        encoding: '@project.build.sourceEncoding@'
        java:
            version: '@java.version@'
        name: '@project.name@'
        version: '@project.version@'

management:
    endpoint:
        health:
            show-details: always
    endpoints:
        web:
            exposure:
                include: '*'

# spring boot admin server
spring:
    boot:
        admin:
            client:
                url: http://localhost:8081
```
