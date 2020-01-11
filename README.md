//Student Regstration Form in jsp

//new.jsp
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<%@page import="java.sql.*" %>
<%
    if(request.getParameter("submit") !=null){
    
        String name = request.getParameter("sname");
        String course = request.getParameter("course");
        String fee = request.getParameter("fee");
        
        Class.forName("com.mysql.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school","root","");
        PreparedStatement pst= con.prepareStatement("insert into records(sname,course,fee)values(?,?,?)");
        ResultSet rs;   
        
        pst.setString(1, name);
        pst.setString(2, course);
        pst.setString(3, fee);
        pst.executeUpdate();
        %>
        
        <script>
            alert("Record Added");
        </script>
        
        <%
        }
%>



<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>JSP Page</title>
        <link href="bootstrap/css/bootstrap.css" rel="stylesheet" type="text/css"/>
        <link href="bootstrap/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>
    </head>
    <body>
        <h1>Student Registration</h1>
        </br>
        <div class="row">
            <!--Form Creation-->
            <div class="col-sm-4">
                <form action="#" method="POST">
                    <div align="left">
                        <lable class="form-label">Student Name</label>
                        <input type="text" class="form-control" placeholder="Student Name" name="sname" id="sname" required>
                        
                    </div>
                    <div align="left">
                        <lable class="form-label">Course</label>
                        <input type="text" class="form-control" placeholder="Course" name="course" id="course" required>
                        
                    </div>
                    <div align="left">
                        <lable class="form-label">Fee</label>
                        <input type="text" class="form-control" placeholder="Fee" name="fee" id="fee" required>
                        
                    </div>
                    </br>
                    <div>
                        <input type="submit" id="submit" value="submit" name="submit" class="btn btn-info" >
                        <input type="reset" id="reset" value="reset" name="reset" class="btn btn-warning" >

                    </div>
                    
                    
                </form>
                
                
            </div>
            <!--Table Creation-->
            <div class="col-sm-8">
                <div class="panel-body">
                    <table id="tbl-student" class="table table-responsive table-bordered" cellpadding="0" width="100%">
                        <thread>
                            <tr>
                                <th>Student Name</th>
                                <th>Course</th>
                                <th>Fee</th>
                                <th>Edit</th>
                                <th>Delete</th>
                            </tr>
                            
                            <% 
                                Class.forName("com.mysql.jdbc.Driver");
                                Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school","root","");
                                PreparedStatement pst= con.prepareStatement("insert into records(sname,course,fee)values(?,?,?)");
                                ResultSet rs;   

                                String query = "select * from records";
                                Statement st = con.createStatement();
                                rs = st.executeQuery(query);
                                
                                   while(rs.next()){
                                   
                                       String id = rs.getString("id");
                                   

                            %>
                            
                            
                            <tr>
                                <td><%=rs.getString("sname")%></td>
                                <td><%=rs.getString("course")%></td>
                                <td><%=rs.getString("fee")%></td>
                                <td><a href="update.jsp?id=<%=id%>">Edit</a></td>
                                <td><a href="delete.jsp?id=<%=id%>">Delete</a></td>
                            </tr>
                            
                        </thread>
                            
                            <%
                                }
                            %>
                            
                    </table>
                </div>
                
            </div>
            
            
        </div>
        
        
        
    </body>
</html>

//update.jsp

<%-- 
    Document   : update
    Created on : Jan 11, 2020, 11:07:42 AM
    Author     : Sandun Sameera
--%>

<%@page contentType="text/html" pageEncoding="UTF-8"%>
<%@page import="java.sql.*" %>
<%
    if(request.getParameter("submit") !=null){
        String id = request.getParameter("id");
        String name = request.getParameter("sname");
        String course = request.getParameter("course");
        String fee = request.getParameter("fee");
        
        Class.forName("com.mysql.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school","root","");
        PreparedStatement pst= con.prepareStatement("update records set sname = ?, course = ?, fee = ? where id = ?");
        ResultSet rs;   
        
        pst.setString(1, name);
        pst.setString(2, course);
        pst.setString(3, fee);
        pst.setString(4, id);
        pst.executeUpdate();
        %>
        
        <script>
            alert("Record Updated");
        </script>
        
        <%
        }
        %>


<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>JSP Page</title>
        <link href="bootstrap/css/bootstrap.css" rel="stylesheet" type="text/css"/>
        <link href="bootstrap/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>
    </head>
    <body>
        <h1>Data Update</h1>
        
        <div class="row">            
               <div class="col-sm-4">
                <form action="#" method="POST">
                    
                    <%
                       Class.forName("com.mysql.jdbc.Driver");
                       Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school","root","");
                       PreparedStatement pst= con.prepareStatement("insert into records(sname,course,fee)values(?,?,?)");
                       ResultSet rs;  

                       String id = request.getParameter("id");
                       pst = con.prepareStatement("select * from records where id = ?");
                       pst.setString(1, id);
                       rs = pst.executeQuery();
                       
                       while(rs.next()){
                        
                    %>
                    
                    <div align="left">
                        <lable class="form-label">Student Name</label>
                        <input type="text" class="form-control" placeholder="Student Name" name="sname" value="<%=rs.getString("sname")%>" id="sname" required>
                        
                    </div>
                    <div align="left">
                        <lable class="form-label">Course</label>
                        <input type="text" class="form-control" placeholder="Course" name="course" value="<%=rs.getString("course")%>" id="course" required>
                        
                    </div>
                    <div align="left">
                        <lable class="form-label">Fee</label>
                        <input type="text" class="form-control" placeholder="Fee" name="fee" value="<%=rs.getString("fee")%>" id="fee" required>
                     </div>
                    
                    <% } %>
                    
                    </br>
                    <div>
                        <input type="submit" id="submit" value="submit" name="submit" class="btn btn-info" >
                        <input type="reset" id="reset" value="reset" name="reset" class="btn btn-warning" >
                    </div>  
                    
                    <div align="right">
                        <p><a href="new.jsp">Back</a></p>
                    </div>
                    
                </form>
            </div>         
            
        </div>
        
    </body>
</html>


//delete.jsp

<%@page import="java.sql.*" %>
<%
        String id = request.getParameter("id");
        
        Class.forName("com.mysql.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school","root","");
        PreparedStatement pst= con.prepareStatement("delete from records where id = ?");
        ResultSet rs;   
        
        pst.setString(1, id);
        pst.executeUpdate();
        %>
        
        <script>
            alert("Record Deleted");
        </script>
        
        <!DOCTYPE html>
        <html>
            <head></head>
            <body>
        
                <div align="left">
                        <h3><a href="new.jsp">Back</a></h3>
                </div>
                
            </body>
        </html>





