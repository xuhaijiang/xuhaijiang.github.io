#### SSL证书用java keytool生成
##### 服务端
1. 生成服务端证书
        keytool -genkey -v -alias tomcat -keyalg RSA -keystore D:/ssl/tomcat.keystore -dname "CN=localhost,OU=xhj,O=xhj,L=hangzhou,ST=Zhejiang,C=CN" -validity 3650 -storepass 123456 -keypass 123456
2. 导出服务端证书
        keytool -export -alias tomcat -keystore D:/ssl/tomcat.keystore -storepass 123456 -rfc -file D:/ssl/tomcat.cer
3. 生成客户端证书
        keytool -genkey -v -alias client -keyalg RSA -keystore D:/ssl/client.keystore -dname "CN=client,OU=xhj,O=xhj,L=hangzhou,ST=Zhejiang,C=CN" -validity 3650 -storepass 123456 -keypass 123456
4. 导出客户端证书
        keytool -export -alias client -keystore D:/ssl/client.keystore -storepass 123456 -rfc -file D:/ssl/client.cer
5. 把客户端证书加入服务端证书信任列表
        keytool -import -file D:/ssl/client.cer -storepass 123456 -keystore D:/ssl/tomcat.truststore -alias client
6. 生成客户端信任列表 （客户端信任的服务端）
        keytool -import -file D:/ssl/tomcat.cer -storepass 123456 -keystore D:/ssl/client.truststore -alias tomcat

##### 浏览器
1. 浏览器证书（已可正常访问）
        keytool -validity 365 -genkeypair -v -alias browser -keyalg RSA -storetype PKCS12 -keystore D:/ssl/browser.p12 -dname "CN=browser,OU=xhj,O=xhj,L=hangzhou,ST=Zhejiang,c=cn" -storepass 123456 -keypass 123456
2. 从客户端证书库中导出客户端证书
        keytool -export -v -alias browser -keystore D:/ssl/browser.p12 -storetype PKCS12 -storepass 123456 -rfc -file D:/ssl/browser.cer
3. 将客户端证书导入到服务器证书库(使得服务器信任客户端证书)
        keytool -import -v -alias browser -file D:/ssl/browser.cer -keystore D:/ssl/tomcat.truststore -storepass 123456
        keytool -list -keystore D:/ssl/tomcat.truststore -storepass 123456
4. 生成jks文件
        keytool -genkey -alias test -keyalg RSA -keypass 123456 -storepass 123456 -dname "CN=client,OU=xhj,O=xhj,L=hangzhou,ST=Zhejiang,C=CN" -validity 3650 -keystore D:/ssl/uac.jks

##### tomcat配置
**server.xml文件：**
          <Connector port="8443"                                            protocol="org.apache.coyote.http11.Http11NioProtocol"
           SSLEnabled="true" maxThreads="150" scheme="https"
           secure="true" clientAuth="true" sslProtocol="TLS"
           keystoreFile="D:\\ssl\\tomcat.keystore" keystorePass="123456"
           truststoreFile="D:\\ssl\\tomcat.truststore" truststorePass="123456" truststoreType="JKS"/>





   
   
   