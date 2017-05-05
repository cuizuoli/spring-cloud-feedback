spring-cloud-feedback
=================
feedback project for [ConsulDiscoveryClient can't get bean ConsulRegistration and ConsulLifecycle in application context.](https://github.com/spring-cloud/spring-cloud-consul/issues/306)

Prepare
-------
* Kafka
* Consul

QuickStart
-----
* configuration consul and kafka
> spring-cloud-feedback/config-server/src/main/resources/application.yml

```
    consul:
      host: 127.0.0.1
      port: 8500
```

> spring-cloud-feedback/web-service/src/main/resources/bootstrap.yml

```
kafka:
  brokers: ${kafka brokers}
  zk-nodes: ${kafka zk-nodes}
  replication-factor: ${kafka replication-factor}
...
    consul:
      host: 127.0.0.1
      port: 8500
```
* Running config-server
* Running web-service (it occurs error)
* added old version dependency
> spring-cloud-feedback/web-service/pom.xml

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-consul-discovery</artifactId>
    <version>1.1.2.RELEASE</version>
</dependency>
```
* Running web-service (it's ok)