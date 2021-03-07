### 1.时区报错
**错误信息：**
```
2019-10-10 10:18:37.245 ERROR 7252 --- [eate-1052241942] com.alibaba.druid.pool.DruidDataSource   : create connection SQLException, url: jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf-8, errorCode 0, state 01S00

java.sql.SQLException: The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:129) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:97) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:89) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:63) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:73) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:76) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.ConnectionImpl.createNewIO(ConnectionImpl.java:835) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.ConnectionImpl.<init>(ConnectionImpl.java:455) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.ConnectionImpl.getInstance(ConnectionImpl.java:240) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.NonRegisteringDriver.connect(NonRegisteringDriver.java:199) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.alibaba.druid.pool.DruidAbstractDataSource.createPhysicalConnection(DruidAbstractDataSource.java:1510) ~[druid-1.1.6.jar:1.1.6]
	at com.alibaba.druid.pool.DruidAbstractDataSource.createPhysicalConnection(DruidAbstractDataSource.java:1575) ~[druid-1.1.6.jar:1.1.6]
	at com.alibaba.druid.pool.DruidDataSource$CreateConnectionThread.run(DruidDataSource.java:2450) ~[druid-1.1.6.jar:1.1.6]
Caused by: com.mysql.cj.exceptions.InvalidConnectionAttributeException: The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
	at sun.reflect.GeneratedConstructorAccessor34.newInstance(Unknown Source) ~[na:na]
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45) ~[na:1.8.0_191]
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423) ~[na:1.8.0_191]
	at com.mysql.cj.exceptions.ExceptionFactory.createException(ExceptionFactory.java:61) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.exceptions.ExceptionFactory.createException(ExceptionFactory.java:85) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.util.TimeUtil.getCanonicalTimezone(TimeUtil.java:132) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.protocol.a.NativeProtocol.configureTimezone(NativeProtocol.java:2241) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.protocol.a.NativeProtocol.initServerSession(NativeProtocol.java:2265) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.ConnectionImpl.initializePropsFromServer(ConnectionImpl.java:1319) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.ConnectionImpl.connectOneTryOnly(ConnectionImpl.java:966) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	at com.mysql.cj.jdbc.ConnectionImpl.createNewIO(ConnectionImpl.java:825) ~[mysql-connector-java-8.0.15.jar:8.0.15]
	... 6 common frames omitted
```


**解决方法**
在数据库连接配置里添加 `serverTimezone=GMT%2B8` 即可


```bash
spring.datasource.url=jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf-8&serverTimezone=GMT%2B8
```

### 2.默认SSL连接

```bash
Establishing SSL connection without server’s identity verification is not recommended. According to MySQL 5.5.45+,
5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn’t set. For compliance 
with existing applications not using SSL the verifyServerCertificate property is set to ‘false’. You need either to explicitly
disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.
```
MySQL 5.5.45+、5.6.26+和5.7.6+的要求，如果没有设置显式选项，则必须默认建立SSL连接
在数据库连接配置里添加`usessl=false`即可




