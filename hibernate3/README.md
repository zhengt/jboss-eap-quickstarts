hibernate3: How to Use  Hibernate 3 in an Application
=====================================================
Author: Bartosz Baranowski   
Level: Intermediate  
Technologies: Hibernate 3  
Summary: The `hibernate3` quickstart is provided to help you understand the changes needed to update your Hibernate 3.x application to use Hibernate 4.  
Target Product: JBoss EAP  
Source: <https://github.com/jboss-developer/jboss-eap-quickstarts/>  

What is it?
-----------

_Note: Hibernate 3.x is not a supported configuration in Red Hat JBoss Enterprise Application Platform 6.1 or later._

The sole purpose of the `hibernate3` quickstart is to help you understand the changes needed to move your application from 
Hibernate 3.x to Hibernate 4 in Red Hat JBoss Enterprise Application Platform. This quickstart has the same functionality as the [hibernate4](../hibernate4/README.md) quickstart 
but uses the Hibernate 3 libraries. Compare this quickstart to the [hibernate4](../hibernate4/README.md) quickstart to see the 
code and class differences between Hibernate 3 and Hibernate 4. 

This quickstart, like the [log4j](../log4j/README.md) quickstart, demonstrates how to define a module dependency. However, this quickstart goes beyond that and also demonstrates the following:
 
* WAR creation - The Maven script and Maven WAR plugin create a *WAR* archive that includes ONLY the Hibernate 3.x binaries. To understand better how this is achieved, please refer to the *pom.xml* in the root directory of this quickstart. Additional information can be found in the <http://maven.apache.org/plugins/maven-war-plugin> documentation.
* Module exclusion and inclusion - This example demonstrates how to control class loading using *dependencies* and *exclusions* in the *jboss-deployment-structure.xml* file. For more information about this file, see the [Red Hat JBoss Enterprise Application Platform Documentation](https://access.redhat.com/documentation/en-US/JBoss_Enterprise_Application_Platform/) _Development Guide_.
* Persistence configuration - Configuration is required to tell the container how to load JPA/Hibernate.
 

_Note: This quickstart uses the H2 database included with Red Hat JBoss Enterprise Application Platform 6. It is a lightweight, relational example datasource that is used for examples only. It is not robust or scalable and should NOT be used in a production environment!_
  
System requirements
-------------------

The application this project produces is designed to be run on Red Hat JBoss Enterprise Application Platform 6.1 or later. 

All you need to build this project is Java 6.0 (Java SDK 1.6) or later, Maven 3.0 or later.

Configure Maven
---------------

If you have not yet done so, you must [Configure Maven](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/CONFIGURE_MAVEN.md#configure-maven-to-build-and-deploy-the-quickstarts) before testing the quickstarts.


Start the JBoss EAP Server
-------------------------

1. Open a command prompt and navigate to the root of the JBoss EAP directory.
2. The following shows the command line to start the server:

        For Linux:   EAP_HOME/bin/standalone.sh
        For Windows: EAP_HOME\bin\standalone.bat

 
Build and Deploy the Quickstart
-------------------------

_NOTE: The following build command assumes you have configured your Maven user settings. If you have not, you must include Maven setting arguments on the command line. See [Build and Deploy the Quickstarts](../README.md#build-and-deploy-the-quickstarts) for complete instructions and additional options._

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean install jboss-as:deploy

4. This will deploy `target/jboss-hibernate3.war` to the running instance of the server.

_Note:_ You will see the following warnings in the server log. 

    These warnings are debugging messages that were fixed for Hibernate 4.x but not backported to Hibernate 3.x. You can ignore these warnings.

        WARN  [org.hibernate.cfg.AnnotationBinder] (ServerService Thread Pool -- 155) Package not found or wo package-info.java: org.jboss.as.quickstart.hibernate3.controller
        WARN  [org.hibernate.cfg.AnnotationBinder] (ServerService Thread Pool -- 155) Package not found or wo package-info.java: org.jboss.as.quickstart.hibernate3.model
        WARN  [org.hibernate.cfg.AnnotationBinder] (ServerService Thread Pool -- 155) Package not found or wo package-info.java: org.jboss.as.quickstart.hibernate3.data
        WARN  [org.hibernate.cfg.AnnotationBinder] (ServerService Thread Pool -- 155) Package not found or wo package-info.java: org.jboss.as.quickstart.hibernate3.util

    These warnings result from Hibernate 3 calling private classes. As noted above, Hibernate 3 is not supported in JBoss EAP 6.1 or later. You can ignore these messages.

        WARN  [org.jboss.as.dependency.private] (MSC service thread 1-6) JBAS018567: Deployment "deployment.jboss-hibernate3.war" is using a private module ("org.apache.commons.collections:main") which may be changed or removed in future versions without notice.
        WARN  [org.jboss.as.dependency.unsupported] (MSC service thread 1-6) JBAS018568: Deployment "deployment.jboss-hibernate3.war" is using an unsupported module ("org.dom4j:main") which may be changed or removed in future versions without notice.
        WARN  [org.jboss.as.dependency.private] (MSC service thread 1-6) JBAS018567: Deployment "deployment.jboss-hibernate3.war" is using a private module ("org.antlr:main") which may be changed or removed in future versions without notice.
        WARN  [org.jboss.as.dependency.private] (MSC service thread 1-6) JBAS018567: Deployment "deployment.jboss-hibernate3.war" is using a private module ("asm.asm:main") which may be changed or removed in future versions without notice.
        WARN  [org.jboss.as.dependency.private] (MSC service thread 1-6) JBAS018567: Deployment "deployment.jboss-hibernate3.war" is using a private module ("org.javassist:main") which may be changed or removed in future versions without notice.


Access the application 
---------------------

The application will be running at the following URL: <http://localhost:8080/jboss-hibernate3/>.


Undeploy the Archive
--------------------

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn jboss-as:undeploy

Run the Quickstart in Red Hat JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts or run the Arquillian tests from Eclipse using JBoss tools. For more information, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JBDS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts) 


Debug the Application
------------------------------------

If you want to debug the source code of any library in the project, run the following command to pull the source into your local repository. The IDE should then detect it.

        mvn dependency:sources


