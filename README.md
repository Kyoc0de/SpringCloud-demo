# SpringCloud-demo
### 微服务模块

- **建模块module**  在父模块下建子模块
- **改pom** 引入dependency
- **写yml**
- **主启动**
- **业务类** 
  * 建表
  * entities
  * dao
  * service
  * controller

---

09-

vue - controller - service - dao - mysql



- [ ] mybatis xml 

- [ ] @Resource 与 @Autowired

---

### 热启动

compiler.automake.allow.when.app.running 

actionSystem.asserFoucusAccessFormEdt 

---

### RestTemplate 提供了多种便携访问远程http服务的方法

是一种简单便捷的访问restful服务模板类,是spring提供的用于访问Rest服务的客户模板工具集

- url Rest请求地址
- requestMap 请求参数
- responseBean.class http响应转换被转换成的对象类型

---

### 工程重构

---

### Eureka

- 什么是服务治理

管理每个服务与服务之间依赖关系比较复杂,管理比较复杂,所以需要使用服务治理,管理服务于服务之间依赖关系,可实现服务调用,负载均衡,容错等,**实现服务发现与注册**

- 什么是服务注册

采用cs设计架构,作为服务注册功能的服务器,它是服务注册中心.

而系统中的其他微服务,使用Eureka的客户端连接到Eureka server并维持心跳连接

这样系统维护人员可以通过Eureka Server来监控系统中各个微服务是否正常运行

**Eureka Server 提供服务注册服务**

各个微服务节点通过配置启动后,会在EurekaServer中进行注册,这样EurekaServer中的服务注册表中将会存储所有可用服务节点的信息,服务节点的信息可以在界面中直观看到

**EurekaClient通过注册中心进行访问**

是一个java客户端,用于简化Eureka Server的互交,客户端同时也具备一个内置的,使用轮询(round-robin)负载算法的负载均衡器.在应用启动后,将会向Eureka server发送心跳默认30s.

如果Eureka Server在多个心跳周期内没有收到节点的心跳,EurekaServer将会从服务注册表中把这个服务节点移除默认90s

```yml
eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false
    fetch-registry: false
    service-url:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaMain7001 {
    public static void main(String[] args) {
        SpringApplication.run(EurekaMain7001.class,args);
    }
}

```

---

注册: @EnableEurekaClient

```yml
eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://localhost:7001/eureka
```



---

- 先启动eureka注册中心
- 启动服务提供者payment支付服务
- 支付服务启动后会把自身信息比如服务地址以别名方式注册金eurake
- 消费者order服务在调用接口时,使用服务别名去注册中心获取实际的RPC远程调用地址
- 消费者获得调用地址后,低层实际是利用httpclient技术实现远程调用
- 消费者获得服务地址后会缓存在本地jvm内存中,默认每间隔30s更新一次服务调用地址

---

### 集群搭建

项目停止
