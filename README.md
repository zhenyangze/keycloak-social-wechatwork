# keycloak-services-social-wechat-work

Keycloak企业微信登录插件

### 版本要求

- Keycloak: 11.03
- Mvn: 3.6.3
- Jdk: 1.8
- infinispan: 9.4.8



### 编译安装

#### 1、打包
`mvn clean package`

#### 2、复制编译文件

To install the social wechat work one has to:

* Add the jar to the Keycloak server (create `providers` folder if needed):
  * `$ cp target/keycloak-services-social-wechat-work-{x.y.z}.jar _KEYCLOAK_HOME_/providers/` 

* Add config page templates to the Keycloak server:
  * `$ cp themes/base/admin/resources/partials/realm-identity-provider-wechat-work.html _KEYCLOAK_HOME_/themes/base/admin/resources/partials/`
  * `$ cp themes/base/admin/resources/partials/realm-identity-provider-wechat-work-ext.html _KEYCLOAK_HOME_/themes/base/admin/resources/partials/`



#### 3、修改jboss依赖 

- change the module.xml,add dependencies items:

`KEYCLOAK_HOME/modules/system/layers/keycloak/org/keycloak/keycloak-services/main/module.xml`

```java
<module name="org.keycloak.keycloak-services" xmlns="urn:jboss:module:1.3">
    <properties>
        <property name="jboss.api" value="private"/>
    </properties>

    <resources>
        <resource-root path="keycloak-services-6.0.1.jar"/>
    </resources>

    <dependencies>
        <module name="org.infinispan" services="import"/>
        <module name="org.keycloak.keycloak-common" services="import"/>
    ...
    </dependencies>
</module>
```

