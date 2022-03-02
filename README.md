# EmployeeForm
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
    <head>
        <style>
            
            
            body{
                background-image: url("images/pk2.jpg");
                background-size: 100%;
                background-position: -400px 0px;
                
                
            }
            div.container{
                width:500px;
                height: 650px;
                margin: 100px auto 0px auto;
            }
            h2{
                text-align: center;
                padding: 20px;
                
            }
            div.container{
                background-color: rgba(0,0,0,0.5);
               
                box-shadow: 2px 2px 15px rgba(0,0,0,0.3);
                color: #fff;
                    
            }
            label
            {
                font-family: sans-serif;
                font-size: 18px;
                font-style:initial;
            }
            input#name{
               
                border: 1px solid #ddd;
                left: 100px;
                border-radius: 3px;
                outline: 0;
                padding: 7px;
                background-color: #fff;
                box-shadow: inset 1px 1px 5px rgba(0,0,0,0.3);
            }
            
        </style>
        <title>Bootstrap Example</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet"
              href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script
        src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script
        src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
        <link rel="stylesheet" href="style.css" type="text/css">
   
    </head>
    <body>
        
        <div class="container">
            <center><h2>Employee Details</h2></center>
            <form id="empForm" method="post">

                <div class="form-group">
                    <label for="name">Employee Name:</label><br>
                    <input type="text" class="form-control" id="name"
                           placeholder="Enter Employee Name" name="name"><br>
                </div>
                <div class="form-group">
                    <label for="email">Email:</label><br>
                    <input type="email" class="form-control" id="email"
                           placeholder="Enter Employee Email" name="email"><br>
                </div>

                <div class="form-group">
                    <label for="Mobile_No">Mobile Number:</label><br>
                    <input type="number" class="form-control" id="Mobile_No"
                           placeholder="Enter Mobile Numbebr" name="Mobile_No"><br>
                </div>
                <div class="form-group">
                    <label for="empsalary">Salary:</label><br>
                    <input type="number" class="form-control" id="empsalary"
                           placeholder="Enter Employee Salary" name="empsalary"><br>
                </div>
                <div class="form-group">
                    <label for="empcity">City:</label><br>
                    <input type="text" class="form-control" id="empcity"
                           placeholder="Enter Employee City" name="empcity"><br>
                </div>

                <input type="button" class="btn btn-primary" id="empSave" value="Save"
                       onclick="saveEmployee();" style="width: 465px; color: black ; background-color: yellow; font-size: 20px;" >
            </form>
        </div>
        <script>
            $("#name").focus();
            function validateAndGetFormData() {

                var empNameVar = $("#name").val();
                if (empNameVar === "") {
                    alert("Employee Name is Required Value");
                    $("#name").focus();
                    return "";
                }
                var empEmailVar = $("#email").val();
                if (empEmailVar === "") {
                    alert("Employee Email is Required Value");
                    $("#email").focus();
                    return "";
                }
                var mobnoVar = $("#Mobile_No").val();
                if (mobnoVar === "") {
                    alert("Mobile Number is Required Value");
                    $("#Mobile_No").focus();
                    return "";
                   
                }
                var esalary = $("#empsalary").val();
                if (esalary === "") {
                    alert("Employee Salary is Required Value");
                    $("#empsalary").focus();
                }
                var ecity = $("#empcity").val();
                if (ecity === "") {
                    alert("Employee city is required value");
                    $("#empcity").focus();
                }

                var jsonStrObj = {
                    name: empNameVar,
                    email: empEmailVar,
                    Mobile_No: mobnoVar,
                    empsalary: esalary,
                    empcity: ecity

                };
                return JSON.stringify(jsonStrObj);
            }
            // This method is used to create PUT Json request.
            function createPUTRequest(connToken, jsonObj, dbName, relName) {
                var putRequest = "{\n"
                        + "\"token\" : \""
                        + connToken
                        + "\","
                        + "\"dbName\": \""
                        + dbName
                        + "\",\n" + "\"cmd\" : \"PUT\",\n"
                        + "\"rel\" : \""
                        + relName + "\","
                        + "\"jsonStr\": \n"
                        + jsonObj
                        + "\n"
                        + "}";
                return putRequest;
            }
            function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
                var url = dbBaseUrl + apiEndPointUrl;
                var jsonObj;
                $.post(url, reqString, function (result) {
                    jsonObj = JSON.parse(result);
                }).fail(function (result) {
                    var dataJsonObj = result.responseText;
                    jsonObj = JSON.parse(dataJsonObj);
                });
                return jsonObj;
            }
            function resetForm() {
                $("#name").val("");
                $("#email").val("");
                $("#Mobile_No").val("");
                $("#empsalary").val("");
                $("#empcity").val("");
                $("#name").focus();
            }
            function saveEmployee() {
                var jsonStr = validateAndGetFormData();
                if (jsonStr === "") {
                    return;
                }
                var putReqStr = createPUTRequest("90938847|-31948835645760697|90945751",
                        jsonStr, "Employee", "Emp-Rel");
                alert(putReqStr);
                jQuery.ajaxSetup({async: false});
                var resultObj = executeCommand(putReqStr,
                        "http://api.login2explore.com:5577", "/api/iml");
                alert(JSON.stringify(resultObj));
                jQuery.ajaxSetup({async: true});
                resetForm();
            }
            
           
        </script>
    </body>
</html>
