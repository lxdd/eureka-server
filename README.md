

#微服务刷新
curl -X POST http://lxdyun.com:8400/refresh



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
