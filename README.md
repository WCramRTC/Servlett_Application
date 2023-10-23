# Servlett_Application

Requirement - Download and Install Java EE ( Enterprise Edition )
 - This comes with the Glassfish server. Which we will use to deploy our servlet.

## [Required: Java EE ( Enterprise Edition ) - Current Version : 8](https://www.oracle.com/java/technologies/javaee-8-sdk-downloads.html)

## [Video Walkthrough : Creating Your Servlet in NetBeans](https://www.youtube.com/watch?v=-gnknflVhcI)

1. Create a new project
2. Choose the Category "Java with Maven"  
    * Followed by Web Application
3. In the Settings, choose the "GlassFish Server"
    * If this is your first time, it may say "No Sever Selected". Click the drop down arrow and you should see it
    * You may get a button asking you to install "GlassFish Server". Click it.
    * If you don't see any server from the drop down, click ***Add*** next to the dropdown. You should see a selection of servers. Choose GlassFish.

    * Jakarata should already be selected for the Java EE Version.

4. Once complete, you should have a new application. Test it by clicking the Run Button ( Green Arrow ). If it works properly, a web browser should appear with "Hello World" displayed.  
The URL will be a LocalHost url, and the name will be the name of your project.