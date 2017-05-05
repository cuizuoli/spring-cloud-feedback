spring-cloud-feedback
=================
:point_right:LMN common module, representing LMN domain model and common enumeration.

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