# web.xml Element Reference
The below example web.xml file (probably) contains an example of every possible element available for use.

This reference is put together mostly from this unofficial resource.

https://wiki.metawerx.net/wiki/Web.xml

I wish I could use some official resource, but the official resources are impenetrable XSD schemas.

```xml
<web-app>
    <!--
        Name of the application.
        This is sometimes seen when using a servlet container's GUI manager.
    -->
    <display-name>AppName</display-name>

    <!--
        Description of the application.

        This is sometimes displayed by a servlet container's admin tools or GUI
        manager.
    -->
    <description>Description of the app</description>

    <!--
        Notifies the application that it will be running in a distributed
        environment (a cluster).

        What this means exactly is that sessions will be shared and synchronized
        across cluster nodes, so requests executing on other members of the
        cluster won't lose session information.
    -->
    <distributable />

    <!-- HTTP session timeout, in minutes -->
    <session-config>
        <session-timeout>120</session-timeout> <!-- 2 hours -->
    </session-config>
</web-app>
```
