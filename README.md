tomcat8-redis-session-manager
============================

基于redis的tomcat8的session同步

## redis配置
*具体配置不详细说明。遵循 [redis官网](http://redis.io/download) 。

## tomcact配置
* 将编译后tomcat-redis-session-manager-1.0.jar拷贝到$TOMCAT_HOME/lib下
    - commons-pool2-2.2.jar
    - jedis-2.5.2.jar
    - tomcat-redis-session-manager-1.0.jar


* 配置参数($TOMCAT_HOME/conf/context.xml文件Context节点下增加如下内容)

         <Valve className="com.whosenet.tomcat.redissessions.RedisSessionHandlerValve" />
         <Manager className="com.whosenet.tomcat.redissessions.RedisSessionManager"
             host="localhost" <!-- optional: defaults to "localhost" -->
             port="6379" <!-- optional: defaults to "6379" -->
             database="0" <!-- optional: defaults to "0" -->
             password="123456" <!--optional: defaults to null-->
             maxInactiveInterval="60" <!-- optional: defaults to "60" (in seconds) -->
             sessionPersistPolicies="PERSIST_POLICY_1,PERSIST_POLICY_2,.." <!-- optional -->
             sentinelMaster="SentinelMasterName" <!-- optional -->
             sentinels="sentinel-host-1:port,sentinel-host-2:port,.." <!-- optional --> />

## 修改内容
* 修改RedisSessionManager.java文件,适应tomcat8。
* 项目构建由gradle改为Maven。

## 注意事项
 - 如果tomcat启动redis-tomcat-session-manager的错误，请将commons-pool2-2.2.jar 和jedis-2.5.2.jar升级到最新稳定版本
 - 如果在JAVA项目中使用setAttribute(Object obj)的时候，其中参数obj必须实现序列化接口，否则属性设置不进去。

## license
* [forked from jcoleman/tomcat-redis-session-manager](http://github.com/jcoleman/tomcat-redis-session-manager)

