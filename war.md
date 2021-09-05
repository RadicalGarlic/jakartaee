# The Web Application Archive (WAR) Format
The servlet specification includes the web application archive (WAR) format. This format specifies a particular directory and file structure that servlet web applications are expected to be in.

The WAR format is as follows.
|Path|Blurb|
|---|---|
|`*.html`, `*.jsp`, etc.|The top level of the directory contains the general files that must be visible to the client (HTML, CSS, images, etc.). Feel free to create some subdirectories to keep it all organized, as long as they don't use the same name as the other top-level directories.|
|`/WEB-INF/web.xml`|The "web application deployment descriptor" file. This file describes all the servlets and other components, along with any initialization parameters.|
|`/WEB-INF/classes/`|Contains any Java class files that are necessary, including a non-servlet classes. The directory structure still needs the follow the package heirarchy though (`mypackage.MyClass` -> `/WEB-INFO/classes/mypackage/MyClass.class`.|
|`/WEB-INF/lib/`|Contains any JARs necessary for the webapp. Third-party JAR libraries would go in here.|

This whole directory can then be compressed into a single ZIP archive and the file extension changed to `.war` in order to signal that the contents of the ZIP archive follow the WAR format. This is very similar to how JAR files work. This single WAR file can usually then be run by servlet containers.

The term "document root" is used to refer to the top-level of the WAR.

## The Web Application Deployment Descriptor (web.xml)
The web application deployment descriptor file is the file at the path `/WEB-INF/web.xml` of the WAR. It describes some general properties of the web applications as well as the servlets that it's comprised of.

Trying to find a reference for this file that is both definitive and readable is proving to be very frustrating. The below links are the best I can find.

https://docs.oracle.com/cd/E13222_01/wls/docs81/webapp/web_xml.html

https://wiki.metawerx.net/wiki/Web.xml

https://jakarta.ee/specifications/servlet/5.0/jakarta-servlet-spec-5.0.html#deployment-descriptor

Below is an example web.xml file. A more complete reference is written up [here](web.xml-reference.md).
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app>
    <!-- General description of the web application -->
    <display-name>My Web Application</display-name>
    <description>This is my web application</description>

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
        Servlet definitions for the servlets that make up your web application,
        including initialization.

        Servlet initialization parameters can be retrieved in servlet code or
        JSP page with the following snippet.
            // "name" should match a <param-name>
            String value = getServletConfig().getInitParameter("name");

        You can define any number of servlets, including zero.
    -->
    <servlet>
        <servlet-name>myServlet</servlet-name>
        <description>My servlet</description>
        <servlet-class>com.mycompany.mypackage.ControllerServlet</servlet-class>
        <init-param>
            <param-name>listOrders</param-name>
            <param-value>com.mycompany.myactions.ListOrdersAction</param-value>
        </init-param>
        <init-param>
            <param-name>saveCustomer</param-name>
            <param-value>com.mycompany.myactions.SaveCustomerAction</param-value>
        </init-param>

        <!--
            Load this servlet at server startup time. Servlets are typically
            loaded upon first request. To avoid this, this element can be
            used to have the servlet load on server startup instead.
            Servlets are loaded in ascending order of the value given to the
            element. The value must be an integer (positive or negative).
        -->
        <load-on-startup>5</load-on-startup>
    </servlet>
    <servlet>
        <servlet-name>myOtherServlet</servlet-name>
        <description>My other servlet</description>
    </servlet>

    <!--
        Define mappings that are used by the servlet container to translate a
        particular request URI (context-relative) to a particular servlet. The
        examples below correspond to the servlet descriptions above.
        
        Thus, a request URI like...
            http://localhost:8080/{contextpath}/myOtherServlet
        ...will be mapped to the "myOtherServlet" servlet.
        
        On the other hand, request like...
            http://localhost:8080/{contextpath}/saveCustomer.do
        ...will be mapped to the "controller" servlet.

        You may define any number of servlet mappings, including zero.
        It is also legal to define more than one mapping for the same
        servlet, if you wish to.
    -->
    <servlet-mapping>
        <servlet-name>myServlet</servlet-name>
        <url-pattern>*.do</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>myOtherServlet</servlet-name>
        <url-pattern>/myOtherServlet</url-pattern>
    </servlet-mapping>

    <!--
        Define the default session timeout for your application, in minutes.
        From a servlet or JSP page, you can modify the timeout for a particular
        session dynamically by using HttpSession.getMaxInactiveInterval().
    -->
    <session-config>
        <!-- 30 minutes -->
        <session-timeout>30</session-timeout>
    </session-config>
</web-app>
```
