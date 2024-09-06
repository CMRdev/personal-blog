- 打开 `apache-tomcat-7.0.96\conf\server.xml` 文件，添加如下配置：

```xml
<Service name="Catalina1">
  <Connector port="8081" protocol="HTTP/1.1"
              connectionTimeout="20000"
              redirectPort="8443" URIEncoding="UTF-8" useBodyEncodingForURI="true"/>
  <Connector port="8010" protocol="AJP/1.3" redirectPort="8443" />
  <Engine name="Catalina1" defaultHost="localhost">
    <Realm className="org.apache.catalina.realm.LockOutRealm">
      <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
              resourceName="UserDatabase"/>
      </Realm>
    <Host name="localhost"  appBase="webapps1/dist"
          unpackWARs="true" autoDeploy="true">
      <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
              prefix="localhost_access_log." suffix=".txt"
              pattern="%h %l %u %t &quot;%r&quot; %s %b" />
        <!-- <Context path="" docBase="/dist" /> -->
    </Host>
  </Engine>
</Service>

<Service name="Catalin2">
  <Connector port="8082" protocol="HTTP/1.1"
              connectionTimeout="20000"
              redirectPort="8443" URIEncoding="UTF-8" useBodyEncodingForURI="true"/>
  <Connector port="8011" protocol="AJP/1.3" redirectPort="8443" />
  <Engine name="Catalina2" defaultHost="localhost">
    <Realm className="org.apache.catalina.realm.LockOutRealm">
      <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
              resourceName="UserDatabase"/>
      </Realm>
    <!-- 注意项目入口文件不可以直接放在dist目录下，而需要嵌套一层目录，如 /dist/pg/index.html -->
    <Host name="localhost"  appBase="webapps2/dist"
          unpackWARs="true" autoDeploy="true">
      <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
              prefix="localhost_access_log." suffix=".txt"
              pattern="%h %l %u %t &quot;%r&quot; %s %b" />
        <!-- <Context path="" docBase="/dist" /> -->
    </Host>
  </Engine>
</Service>
```
