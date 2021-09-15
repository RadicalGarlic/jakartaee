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

    <!--
        <taglib> Specifies where to load tag libraries for us in JSP.

        Up until Tomcat7 (2011), <taglib> did not need to be enclosed in
        <jsp-config>.

        Since JSP 2.0 (2003), <taglib> is now optional since tag library files
        (*.tld) are now automatically the webapp's WEB-INF, every subdirectory
        of WEB-INF, and inside each JAR in WEB-INF/lib. The JAR file should be
        packaged like below.
            META-INF/*.tld
            mypackages/MyClasses.class

        The <taglib-uri> element provides an identifier that allows the tag
        library to be used in JSP files like so.
            <%@ taglib prefix="mn" uri="metawerx-networking" %>
            <mn:sometag>Test</mn:sometag>
            <mn:othertag />
    -->
    <jsp-config>
        <taglib>
            <taglib-uri>mytags</taglib-uri>
            <taglib-location>/WEB-INF/jsp/mytaglib.tld</taglib-location>
        </taglib>
    </jsp-config>

    <!--
        <jsp-property-group> specifies additional properties for the JSP files
        specified by <url-pattern>.

        In the below example, a header and footer are applied to every JSP file
        in the webapp. This is equivalent to placing
        <%@ include file="header.jsp" %> and <%@ include file="footer.jsp" %> at
        the top and bottom of every JSP file.
    -->
    <jsp-config>
        <jsp-property-group>
            <url-pattern>*.jsp</url-pattern>
            <include-prelude>/WEB-INF/jspf/header.jspf</include-prelude>
            <include-coda>/WEB-INF/jspf/footer.jspf</include-coda>
        </jsp-property-group>
    </jsp-config>

    <!--
        Context initialization parameters that define shared string constants
        for the entire application. The term "context" is used to refer to the
        web application itself.

        They can be read using JSP or servlet code by using the following.
            // "name" should match a <param-name>
            String val = getServletContext().getInitParameter("name");

        You can define any number of context initialization
        parameters, including zero.
    -->
    <context-param>
        <param-name>SomeParam</param-name>
        <param-value>SomParamValue</param-value>
        <description>Some parameter</description>
    </context-param>

    <!--
        Sets the environment variables (properties) that can be later accessed
        using JNDI.

        The type is usually java.lang.String, but can be any fully qualified
        class name.
    -->
    <env-entry>
        <env-entry-name>key</env-entry-name>
        <env-entry-value>value</env-entry-value>
        <env-entry-type>java.lang.String</env-entry-type>
    </env-entry>
    <env-entry>
        <env-entry-name>anotherKey</env-entry-name>
        <env-entry-value>anotherValue</env-entry-value>
        <env-entry-type>java.lang.String</env-entry-type>
    </env-entry>
</web-app>
```
