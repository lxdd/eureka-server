# autobot-developer-center
汽车人开发者中心

#生成非对称秘钥
$ keytool -genkeypair -alias mytestkey -keyalg RSA \
  -dname "CN=Web Server,OU=Unit,O=Organization,L=City,S=State,C=US" \
  -keypass changeme -keystore server.jks -storepass letmein

#config-server 自查路径
http://localhost:8402/autobot-res/dev/master
#config 加密、解密
curl -u user:37cc5635-559b-4e6f-b633-7e932b813f73  http://localhost:8402/encrypt -d lxdyun
curl -u user:37cc5635-559b-4e6f-b633-7e932b813f73 localhost:8402/decrypt -d AQA7cWTu/90Vev/6hg/bifObcROIfDKyxcPvdPqVXH4y2VAv4js0zZIW6OMMJ/wUOATlpwDJ+4NG+0OAPWAaWSSg/YWYqdi1eV+3MoeYx3jVSUxBpjRX1yyd590D+JuyBVNiVFmMc5kRCbw2AviMX0cpRYGCEfXcKsvoICjmb2iUo9RMcvrEcgEpoEu2sLy4uGzfPWSxmO06Y/CF2ds+9Vk9/HxtWYiHmsYq9skY1FserOeJRUvS25s1DyKKTr63zOc7MF1hHb46A4YY0eJdbZ+l4Dh6Vx0hL3gqHutPxK3JWBwBjvJGXr5gj8d2HaV/34ytpo3J+s9HbqDWwegEftLUYBPPdoRb39tVIr44I58M3nzQ/iz7UOI7sCCAIGcdp1U=

#微服务刷新
curl -X POST http://lxdyun.com:8400/refresh


#swagger 
http://localhost:8400/swagger-ui.html



#网关zuul  
类似于面向对象设计模式中的Facade模式， 它的存在就像是整个微服务架构系统的门面一样，所有的外部客户端访问都需要经过它来进行调度和过滤。
它除了要实现请求路由、 负载均衡、 校验过滤等功能之外， 还需要更多能力， 比如与服务治理框架的结合、 请求转发时的熔断机制、 服务的聚合等一系列高级功能。将自身注册为Eureka服务治理下的应用， 同时从Eureka中获得了所有其他微服务的实例信息。 这样的设计非常巧妙地将服务治理体系中维护的实例信息利用起来， 使得将维护服务实例的工作交给了服务治理框架自动完成， 不再需要人工介入。
1、用户登录状态token
2、签名校验的机制（为了防止客户端在发起请求时被篡改等安全方面的考虑）





一、文档
1、ADC接入 签名方式约定
2、非ADC接口接入 签名方式约定

二、项目接入及改造
1、新的独立项目直接作为微服务加入并提供HTTP接口

2、原项目接入方式（1、改造原项目提供出HTTP能力；2、开发适配器类似注解方式，方案待研究讨论）

3、是否有必要改造，以及新项目是否采用微服务来做

4、新老项目适配互相能调用（HTTP体系与RPC体系 只通过开发适配器是否可行性调研）

三、
1、文档与服务多对多，文章接口改造；（OK）
2、ADC过滤器签名验证逻辑（OK）
3、过滤器取 APP 信息加入签名验证 并出签名文档。（OK）
4、ADC后端目录接口编辑 （OK）
5、发布正式环境
6、暴露一个对外的HTTP服务接口 对外校验里多个method，用于查找资源表信息（拿VIN码反查或者bcar中造个例子） 
7、对外hTTP接口method重定向

四、ADC联调
8、文档管理根据serveId查询文档列表
9、文档管理 删除文档时一并删除关系表
10、文档列表接口优化改造


spring-cloud 微服务组件demo

1、list copy； 
2、eureka 红色告警; 
3、mybatis官网看看;
4、分布式启动；
5、负载均衡测试；
6、注册中心高可用命令启动; 
7、微服务架构事务怎么控制; 
8、OGNL表达式、Spring EL ; 
9、html5（HTML5规范要求⽤户⾃定义属性以data-前缀开头） ； 
10、java Bean、EJB、POJO；11、PO； 12、VO、13、DTO；

**工程名**	**描述**	**端口**
zipkin-server 链路追踪 9411
config-server	配置管理中心	8402
eureka-server	服务发现与注册中心	8404
hystrix-dashboard	监控	

api-gateway	服务网关	8401
autobot-res	ADC 	8400

常用命令：
本地仓库 的更新
mvn -X  clean package install 
远程 仓库 的更新
mvn clean package deploy
打包
mvn package

xmls阿里云不挂断运行命令 nohup java -jar XXX.jar & 
1. 查看端口号占用情况：netstat -apn|grep 80 (ESTABLISHED6426/lighttpd)
2. 确定进程号: ps -aux|grep <进程号> 
3. 杀掉该进程 : kill -9 

发布流程：
一、Spring Cloud Eureka 注册中心
1、根目录下生成可执行jar：mvn package 
2、Linux hosts配置
127.0.0.1	eureka1
127.0.0.1	eureka2
3、上传Linux
4、执行 spring boot启动命令：
nohup java -jar eureka-server-1.0.0-SNAPSHOT.jar --spring.profiles.active=eureka1 & 
nohup java -jar eureka-server-1.0.0-SNAPSHOT.jar --spring.profiles.active=eureka2 & 
5、查看启动端口
netstat -apn|grep 80 (ESTABLISHED6426/lighttpd)
6、查看发布
http://lxdyun.com:8404/
http://lxdyun.com:8405/

二、Spring Cloud Config 配置中心 
1、打包
2、上传
3、启动
nohup java -jar config-server-0.0.1-SNAPSHOT.jar & 
4、查看发布
http://lxdyun.com:8402/autobot-res/dev/

三、Spring Cloud zipkin
http://lxdyun.com:9411

四、业务微服务ADC
http://lxdyun.com:8400/swagger-ui.html
