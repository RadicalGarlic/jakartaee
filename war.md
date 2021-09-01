# The Web Application Archive (WAR) Format
The servlet specification includes the web application archive (WAR) format. This format specifies a particular directory and file structure that servlet web applications are expected to be in.

The WAR format is as follows.
|Path|Blurb|
|---|---|
|`\*.html`, `\*.jsp`, etc.|The top level of the directory contains the general files that must be visible to the client (HTML, CSS, images, etc.). Feel free to create some subdirectories to keep it all organized, as long as they don't use the same name as the other top-level directories.|
|`/WEB-INF/web.xml`|The "web application deployment descriptor" file. This file describes all the servlets and other components, along with any initialization parameters.|
|`/WEB-INF/classes/`|Contains any Java class files that are necessary, including a non-servlet classes. The directory structure still needs the follow the package heirarchy though (`mypackage.MyClass` -> `/WEB-INFO/classes/mypackage/MyClass.class`.|
|`/WEB-INF/lib/`|Contains any JARs necessary for the webapp. Third-party JAR libraries would go in here.|

This whole directory can then be compressed into a single ZIP archive and the file extension changed to `.war` in order to signal that the contents of the ZIP archive follow the WAR format. This is very similar to how JAR files work. This single WAR file can usually then be run by servlet containers.

The term "document root" is used to refer to the top-level of the WAR.
