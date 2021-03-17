Spring Cloud Netflix Eureka (Server)
==========

# 1. build.gradle
> 버전  
- spring cloud: 2020.0.1  
- spring-cloud-starter-netflix-eureka-server: 3.0.1

> dependencies 추가
- org.springframework.cloud:spring-cloud-starter-netflix-eureka-server

```text
ext {
	set('springCloudVersion', "2020.0.1")
}

dependencies {
	implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-server'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

dependencyManagement {
	imports {
		mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
	}
}
```

# 2. Application.yml

> 서버 포트 설정
```yaml
server:
  port: 8761
```

> eureka 설정
- eureka.instance.hostname: eureka server hostname 작성
- eureka.client.serviceUrl.defaultZone: DefaultZone Url 설정을 통해 동일한 zone의 eureka server clustering 설정
- register-with-eureka: 본인 서비스를 eureka 서버에 등록 할지 여부.(eureka는 서버이면서 client가 될 수도 있음)
- fetch-registry: eureka 서버로 부터 서비스 리스트 정보를 local에 caching 할지 여부

```yaml
eureka:
  instance:
    hostname: 127.0.0.1
  client:
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
    register-with-eureka: false
    fetch-registry: false

```

# 3. Code

> @EnableEurekaServer 추가
```java
@EnableEurekaServer
@SpringBootApplication
public class EurekaServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(EurekaServerApplication.class, args);
	}

}
```