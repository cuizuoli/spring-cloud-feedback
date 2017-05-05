spring-cloud-feedback
=================
feedback project for [#306 ConsulDiscoveryClient can't get bean ConsulRegistration and ConsulLifecycle in application context.](https://github.com/spring-cloud/spring-cloud-consul/issues/306)

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
```
2017-05-05 16:37:28,791 ERROR task-scheduler-7 o.s.c.n.h.s.HystrixStreamTask:368 - Error adding metrics to queue
java.lang.IllegalStateException: Must have one of ConsulRegistration or ConsulLifecycle
	at org.springframework.cloud.consul.discovery.ConsulDiscoveryClientConfiguration$LifecycleRegistrationResolver.getInstanceId(ConsulDiscoveryClientConfiguration.java:95) ~[spring-cloud-consul-discovery-1.2.0.RELEASE.jar:1.2.0.RELEASE]
	at org.springframework.cloud.consul.discovery.ConsulDiscoveryClient.getLocalServiceInstance(ConsulDiscoveryClient.java:95) ~[spring-cloud-consul-discovery-1.2.0.RELEASE.jar:1.2.0.RELEASE]
	at org.springframework.cloud.netflix.hystrix.stream.HystrixStreamTask.gatherMetrics(HystrixStreamTask.java:120) ~[spring-cloud-netflix-hystrix-stream-1.3.0.RELEASE.jar:1.3.0.RELEASE]
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:1.8.0_45]
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[na:1.8.0_45]
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:1.8.0_45]
	at java.lang.reflect.Method.invoke(Method.java:497) ~[na:1.8.0_45]
	at org.springframework.scheduling.support.ScheduledMethodRunnable.run(ScheduledMethodRunnable.java:65) [spring-context-4.3.7.RELEASE.jar:4.3.7.RELEASE]
	at org.springframework.scheduling.support.DelegatingErrorHandlingRunnable.run(DelegatingErrorHandlingRunnable.java:54) [spring-context-4.3.7.RELEASE.jar:4.3.7.RELEASE]
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511) [na:1.8.0_45]
	at java.util.concurrent.FutureTask.runAndReset(FutureTask.java:308) [na:1.8.0_45]
	at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.access$301(ScheduledThreadPoolExecutor.java:180) [na:1.8.0_45]
	at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:294) [na:1.8.0_45]
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142) [na:1.8.0_45]
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617) [na:1.8.0_45]
	at java.lang.Thread.run(Thread.java:745) [na:1.8.0_45]
```
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