# Oracle WebLogic tips

> All tips are for a Linux environment.

&nbsp;

:construction: Activate the debug mode permanently on a local domain:
- open the `setDomainEnv.sh` file for the domain
- locate and uncomment the following lines:
```
debugFlag="true"
export debugFlag
```

&nbsp;

:scroll: Configure a WAR to be able to use SLF4J without conflicting with WebLogic's version of SLF4J :
- if not already done, create a `weblogic.xml` file in `WEB-INF` directory
- add the two following `prefer-application-*` blocks to your `weblogic.xml`:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<weblogic-web-app xmlns="http://xmlns.oracle.com/weblogic/weblogic-web-app"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                  xsi:schemaLocation="http://xmlns.oracle.com/weblogic/weblogic-web-app http://xmlns.oracle.com/weblogic/weblogic-web-app/1.4/weblogic-web-app.xsd">

    <container-descriptor>
        
        <!-- make it possible to use SLF4J without conflicting with WebLogic's version of SLF4J -->
        <prefer-application-packages>
            <package-name>org.slf4j.*</package-name>
        </prefer-application-packages>
        
        <!-- prevent SLF4J from displaying a warning about multiple bindings -->
        <prefer-application-resources>
            <resource-name>org/slf4j/impl/StaticLoggerBinder.class</resource-name>
        </prefer-application-resources>
        
    </container-descriptor>

</weblogic-web-app>
```

&nbsp;

:key: Default _KeyStore_ and _TrustStore_ present in a WebLogic 12 instance:

- _KeyStore_ : private key and identity certificates
  - JKS file location: `${DOMAIN_HOME}/security/DemoIdentity.jks`
  - store password: `DemoIdentityKeyStorePassPhrase`
  - private key password: `DemoIdentityPassPhrase`
  
- _TrustStore_ : certificates from Certified Authorities (CA)
  - JKS file location: `${WEBLOGIC_HOME}/wlserver/server/lib/DemoTrust.jks`
  - store password: `DemoTrustKeyStorePassPhrase`
