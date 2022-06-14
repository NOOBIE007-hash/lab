https://github.com/NOOBIE007-hash/lab.git


 String url = "jdbc:mysql://localhost:3306/test_db";
        String user = "root";
        String password = "cricket 10";
        Class.forName("com.mysql.cj.jdbc.Driver").newInstance();
        System.out.println("Model called");
        Connection con = DriverManager.getConnection(url, user, password);
        System.out.println("con--->"+con);
        Statement st = con.createStatement();
        System.out.println("uname passwd Received from controller is " + uname + "  " + pwd);
        String s = "select * from users where uname = \'" + uname + "\' AND pwd = \'"+pwd+"\';";
        System.out.println(s);
        ResultSet rs = st.executeQuery(s);
        int ok = 0;
        if(rs.next()){
           ok = 1; 
        }
        while(rs.next())
        {
            System.out.println(rs.getString(1)+ "   " + rs.getString(2));
        }
     
     
     
     package questionController;
import questionModel.question_model;
import java.util.*;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class questionaction extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res){
      try{  
            System.out.println("question controller called");
            String uname = req.getParameter("name");
            String lang = req.getParameter("lang");
            System.out.println(uname + ' ' + lang);
            question_model qm = new question_model();
            String resp = qm.getQuestion(lang);
            System.out.println(resp);
            String reqdAnswers = qm.answerList;
            res.setContentType("text/html");
            PrintWriter out = res.getWriter();
            int cnt = 0;
            for(int j = 0; j < resp.length; ++j){
                for(int i = 0; i < answerList.length; ++i) {
                    if(answerList[i] == req.getParameter("q" + toString(i+1))){
                        ++cnt;
                    }
                }
                out.writeln(cnt + '/' + 2);
            }
        } catch(Exception E) {
            System.out.println(E);
        }
    }
}



package signupModel;
import java.io.*;
import java.util.*;
import java.sql.*;
// import java.lang.*;
public class signup_model {
    public int getUsers(String uname, String pwd) throws Exception {
        String url = "jdbc:mysql://localhost:3306/test_db"; 
        String user = "root";
        String password = "cricket 10";
        Class.forName("com.mysql.cj.jdbc.Driver").newInstance();
        System.out.println("signup Model called");
        Connection con = DriverManager.getConnection(url, user, password);
        System.out.println("con--->"+con);
        Statement st = con.createStatement();
        Statement st1 = con.createStatement();
        System.out.println("uname passwd Received from controller is " + uname + "  " + pwd);
        String s = "select * from users where uname = \'" + uname + "\' AND pwd = \'"+pwd+"\';";
        System.out.println(s);
        ResultSet rs = st.executeQuery(s);
        int ok = 0;
        if(rs.next()){
           ok = 1; 
           s = "insert into users values(" + "\'" + uname + "\' , " + "\'" + pwd + "\');";
           System.out.println(s);
           st1.executeUpdate(s);
        }
        while(rs.next())
        {
            System.out.println(rs.getString(1)+ "   " + rs.getString(2));
        }
        return ok;
    }
}



    <form action="question" method = "get">
        <label for = "name">Your name</label>
        <input type="text" id = "name" name = "name" onfocus="changeBorder(this)" oninvalid="alert('You must fillll out this field!');" onblur="resetColor(this)" pattern="[A-Za-z]+" required><br>
        
        <label for = "college">Your college</label>
        <input type="text" id = "college" name = "college" onfocus="changeBorder(this)" oninvalid="alert('You must fill out this field!');" onblur="resetColor(this)" pattern="[A-Za-z]+" required><br>
        
        <label for = "address">Your address</label>
        <input type="text" id = "address" name = "address" onselect="changeBorder(this)" onblur="resetColor(this)" pattern="[A-Za-z0-9 ]*"><br>
        
        <label for = "pin">Your PIN Code</label>
        <input type="text" id = "pin" name="pin" pattern="[0-9]{1-6}"  required><br>
        
        <label for = "age">Your Age</label>
        <input type="text" id = "age" name ="age" onkeypress="alert('Enter Age')" pattern="[0-9]*"><br>
        
        <label for = "datee">Your DOB</label>
        <input type="date" id = "datee" name="datee" required="required"><br>
        
        <p>Enter gender</p>
        <label for="male">Male</label>
        <input type="radio" id="male" name="gender" onclick="setGender('male')">
        <label for="female">female</label>
        <input type="radio" id="female" name="gender" onclick="setGender('female')"" required>
        <label for="other">Not specified</label>
        <input type="radio" id="other" name="gender" onclick="setGender('other')" ><br>
        
        <label for="dept">Choose a department:</label>
            <select name="dept" onchange="setDept(this.value)" id="dept" form="deptform" required><option value="cse">CSE</option>
            <option value="it">IT</option>
            <option value="ece">ECE</option>
            <option value="mech">Mech</option>
       
        </select><br><br>
        
        <label for="tel">Your phone number</label>
        <input type="text" id="tel" name="tel" oninvalid="alert('You must fill out this field!');" pattern="[0-9]{10}" />
        <br><br>
        
        <label for = "email">Your email</label>
        <input type="email" name="email" id = "email"  required><br>
        
        <input type="checkbox" id="cycling" name="cycling" value="Cycling" onclick="check(this.value)">
        <label for="cycling"> Cycling</label><br>
        <input type="checkbox" id="guitar" name="guitar" value="guitar" onclick="check(this.value)">
        <label for="guitar"> Guitar</label><br>
        <input type="checkbox" id="juggling" name="juggling" value="juggling" onclick="check(this.value)">
        <label for="juggling"> Juggling</label><br><br>
        
        <label for="prog">Programming Skills</label>
        <input type="text" name="prog" id="prog" ondrop="drop(event)" ondragover="allowDrop(event)">
        <ul>
            <li id="l1" draggable="true" ondragstart="drag(event)" >C++ </li>
            <li id="l2" draggable="true" ondragstart="drag(event)" >C </li>
            <li id="l3" draggable="true" ondragstart="drag(event)" >Python </li>
        </ul>
        
        <label for="myfile">Select a file:</label>
        <input type="file" id="myfile" name="myfile"><br><br>
        
        <input type="submit" onclick="tabulate()"  value="submit">
        <input type="reset"> 

        <div id="tab"></div>
    </form>
    
    
    
    !DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login page</title>
</head>
<body>
    <h1>loginpage</h1>
    <form action="login" method="get">
        Enter your username<input type="text" name="uname"><br>
        Enter your password <input type = "text" name = "pwd"><br>
        <input type="submit" value="Log in">
    </form><br>
    <button onclick="location.href = 'index.html'">Return to home screen</button>

</body>
</html>


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login page</title>
</head>
<body>
    <h1>Welcome to programming test</h1>
    <h3>Login if you are an existing user, else sign up!</h3>
    <button onclick="location.href='login.html'">Login</button>
    <button onclick="location.href='signup.html'">Sign up</button>
</body>
</html>


 <link rel="stylesheet" href="style.css">
 
   <script src="app.js"></script>



