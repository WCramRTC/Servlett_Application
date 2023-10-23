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

---
## Geeks For Geeks Tutorial : Implementing and Walk Through

The Geeks for Geeks website has a great introduction to one of the main purposed of using a Servlet, helping connect front and back end web services for relaying data.

You are welcome to walk through the whole tutorial if you are interested in servlets, but we're gonna quickly implent their code in our projects, and then deconstruct to understand what they did.

## [Geeks For Geeks : Servlet - Form Data](https://www.geeksforgeeks.org/servlet-form-data/)  
***If you use the code from Geeks For Geeks, some of it is outdated.  
You will have to replace `javax` with `jakarta` in the importants to remove the errors***

## Step 1 - Create a Details.html page

1. In the `Web Pages` folder you are going to add a new webpage.
2. Right click on the `Web Pages` folder, hover over new, and selected `html`
3. Give it the name `Details`

You should now have a `Details.html` page in your `Web Pages` folder. It'll be right next to the `index.html` page.

### *** Test your code : Step 1 ***
Run your project. At the end of the URL in the browser add `Details.html`. And hit enter  
Example : `http://localhost:8080/Servlett_Application/Details.html`

If it works, you should see a new page with the phrase TODO list appear.

## Step 2 - Replace the html

GfG's provides the following code for the `Details.html` we just created. Copy and replace all the code in your `Details` with this code.

--- 

```html
<!DOCTYPE html> 
<html> 
<head> 
<meta charset="ISO-8859-1"> 
<title>User Details</title> 
</head> 
<body > 
    <h3>Fill in the Form</h3> 
  
    <form action="FormData" method="post"> 
        <table> 
  
            <tr> 
                <td>Full Name:</td> 
                <td><input type="text" name="name" /></td> 
            </tr> 
            <tr> 
                <td>Phone Number:</td> 
                <td><input type="text" name="phone" /></td> 
            </tr> 
            <tr> 
                <td>Gender:</td> 
                <td><input type="radio" name="gender" value="male" />Male  
                    <input type="radio" name="gender" value="female" />Female</td> 
            </tr> 
            <tr> 
                <td>Select Programming Languages to learn:</td> 
                <td><input type="checkbox" name="language" value="java" />Java 
                    <input type="checkbox" name="language" value="python" />Python 
                    <input type="checkbox" name="language" value="sql" />SQL 
                    <input type="checkbox" name="language" value="php" />PHP</td> 
            </tr> 
            <tr> 
                <td>Select Course duration:</td> 
                <td><select name="duration"> 
                    <option value="3months">3 Months</option> 
                    <option value="6months">6 Months</option> 
                    <option value="9months">9 Months</option></select></td> 
            </tr> 
            <tr> 
                <td>Anything else you want to share:</td> 
                <td><textarea rows="5" cols="40" name="comment"></textarea></td> 
            </tr> 
  
        </table> 
  
        <input type="submit" value="Submit Details"> 
  
    </form> 
  
</body> 
</html>
```
--- 

### *** Test your code : Step 2 ***
Run your project again, and add `Details.html` like before. The webpage should now display the form code from the html we replaced.

--- 

## Step 3 - Adding a FormDataHandle.java page

This next step will help us create the **back end code** for our servlet. 

1. Click the arrow next to `Source Packages`, then right click on the package that has your name, and the project name on it.  
Example, my package name is `com.wcram.servlett_application`.

You should find a `JakartaRestConfiguration.java` file in there.

2. Select **New** then **Java class**.

3. Give your class the name **FormDataHandle**. This is important to get accurate. Otherwise you'll get errors on the next step.

4. Next, copy and paste the following code into your `FormDataHandle.java`.  
***Do not replace the package at the top of your page***

---
```java
import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException; 
import java.io.PrintWriter; 
  
// Servlet implementation class FormDataHandle 
  
// Annotation to map the Servlet URL 
@WebServlet("/FormData") 
public class FormDataHandle extends HttpServlet { 
    private static final long serialVersionUID = 1L; 
  
    // Auto-generated constructor stub 
    public FormDataHandle() { 
        super(); 
    } 
  
    // HttpServlet doPost(HttpServletRequest request, HttpServletResponse response) method 
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
          
        // Get the values from the request using 'getParameter' 
        String name = request.getParameter("name"); 
        String phNum = request.getParameter("phone"); 
        String gender = request.getParameter("gender"); 
          
        // To get all the values selected for  
        // programming language, use 'getParameterValues' 
        String progLang[] = request.getParameterValues("language"); 
        
        // Iterate through the String array to  
        // store the selected values in form of String 
        String langSelect = ""; 
        if(progLang!=null){ 
            for(int i=0;i<progLang.length;i++){ 
                langSelect= langSelect + progLang[i]+ ", "; 
            } 
        } 
          
        String courseDur = request.getParameter("duration"); 
        String comment = request.getParameter("comment"); 
                  
        // set the content type of response to 'text/html' 
        response.setContentType("text/html"); 
          
        // Get the PrintWriter object to write  
        // the response to the text-output stream 
        PrintWriter out = response.getWriter(); 
          
        // Print the data 
        out.print("<html><body>"); 
        out.print("<h3>Details Entered</h3><br/>"); 
          
        out.print("Full Name: "+ name + "<br/>"); 
        out.print("Phone Number: "+ phNum +"<br/>"); 
        out.print("Gender: "+ gender +"<br/>"); 
        out.print("Programming languages selected: "+ langSelect +"<br/>"); 
        out.print("Duration of course: "+ courseDur+"<br/>"); 
        out.print("Comments: "+ comment); 
          
        out.print("</body></html>"); 
          
    } 
  
}
```
---
### *** Test your code : Step 3 ***
Run your project again, and go to the `Details.html` page again. This time enter in data into some of the text boxes and then click the submit button.

You should be redirected to a new webpage called `FormData.html` and your data should appear. This was done with our servlet.

We'll break down what's happening next.

---

## Walking through our code