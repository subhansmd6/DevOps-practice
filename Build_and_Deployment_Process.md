# Build and Deployment Process Using Two Servers

This document describes the step-by-step process for setting up a Build
Server and a Deployment Server for Java web application deployment using
Maven and Tomcat. The Build Server handles code compilation and WAR
creation, while the Deployment Server hosts the application using Apache
Tomcat.

## Server Setup Overview

1\. Build Server: Used to build and create the artifact (.war file).

\- Install Java and Maven.

2\. Deploy Server: Used to deploy and host the application using Tomcat.

\- Install Java and Tomcat.

## Step-by-Step Process

1.  Install Java on Build Server

    ![](media/image1.JPG){width="6.0in" height="1.4166666666666667in"}

2.  Install Maven on Build Server

    ![](media/image2.JPG){width="6.423611111111111in"
    height="2.2847222222222223in"}

3.  Clone the code repository from GitHub on Build server

    ![](media/image3.JPG){width="6.0in" height="1.398611111111111in"}

    Now check, whether you have cloned the code and pom.xml file exists.

    ![](media/image4.JPG){width="5.027777777777778in"
    height="1.4861111111111112in"}

4.  Build the artifact using "mvn package" command, then you can see the
    output as below

    ![](media/image5.JPG){width="6.0in" height="2.03125in"}

5.  Install Java on Deploy server using command "sudo apt install
    openjdk-17-jre-headless" (Same way we have installed java on Build
    server)

6.  Install Tomcat on the Deploy Server

-   Go to Apache tomcat official website

-   Copy the tar extension file url link

-   Download it using wget command followed by the url link

-   After downloading tar file, extract the tar file using "tar -xvf
    apache-tomcat-9.0.110.tar.gz" command

    ![](media/image6.JPG){width="6.666666666666667in"
    height="2.4791666666666665in"}

7.  Configure "webapps/host-manager/META-INF/context.xml" on the Deploy
    Server

-   After opening the context.xml file, locate the following lines

    \<Valve className=\"org.apache.catalina.valves.RemoteAddrValve\"

    allow=\"127\\.\\d+\\.\\d+\\.\\d+\|::1\|0:0:0:0:0:0:0:1\" and comment
    it out by enclosing it within \<!\-- and \--\> tags.

    ![](media/image7.JPG){width="6.0in" height="0.35138888888888886in"}

8.  Configure webapps/manager/META-INF/context.xml on the Deploy Server.

    This step is the same as the previous one, but here you need to
    modify the context.xml file located in webapps/manager/META-INF/.

9.  Configure conf/tomcat-users.xml on the Deploy Server with
    appropriate roles and users

-   After opening file, locate for roles lines which are pre-defined and
    commented, those lines should be uncommented and passwords should be
    changed.

    ![](media/image8.JPG){width="6.0in" height="0.6340277777777777in"}

10. Start the Tomcat service on the Deploy Server by changing to "bin"
    directory

    ![](media/image9.JPG){width="6.0in" height="1.81875in"}

11. Allow inbound rules for port 8080 on the Deploy Server in AWS
    security groups

    ![](media/image10.JPG){width="6.0in" height="2.2354166666666666in"}

12. Access the Tomcat web interface on the browser using the public IP
    of the Deploy Server.

    ![](media/image11.JPG){width="6.0in" height="2.357638888888889in"}

13. Now, to copy the .war artifact from Build server to Deploy server
    you need to connect both the servers through ssh keys.

    Create ssh keys using "ssh-keygen" command on Build server

    Copy the public keys "id_rsa.pub" of Build server

    ![](media/image12.JPG){width="6.0in" height="1.1125in"}

    Paste the copied public keys of build server to authorized keys (by
    changing to .ssh directory) of Deploy server

    ![](media/image13.JPG){width="6.0in" height="1.1875in"}

14. Copy the .war file from the Build Server to the Deploy Server using
    SCP command

    ![](media/image14.JPG){width="6.0in" height="0.8618055555555556in"}

15. Verify that the .war file has been copied to /opt/tomcat/webapps/ on
    the Deploy Server

    ![](media/image15.JPG){width="6.0in" height="0.40902777777777777in"}

16. Access the deployed application through the browser using the public
    IP of the Deploy Server.

    ![](media/image16.JPG){width="6.0in" height="2.3958333333333335in"}
