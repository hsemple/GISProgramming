---
permalink:  /javascript/
title: "Introduction to JavaScript"
sidebar:
  nav: "docs"
---



### What is JavaScript?

JavaScript is a web programming language that is used to make web pages interactive.  Typically, JavaScript code is inserted 
into the HTML. Script tags are used to separate the JavaScript code from HTML.  In web map programming, we use JavaScript to 
interact with map libraries and with HTML objects.

 
<br>
 

#### A Simple JavaScript Program

This program below shows how a web page can be made interactive by including JavaScript in the HTML.  The interaction occurs
because users can enter data into the HTML form and receive feedback in the form of calculation results from the application:

First, the program will prompt the user with two pop-up windows, one right after the other. Both will prompt the user to enter a number.
Secondly, the program will check the two values to verify that they are integers.
Third, the program will add the integers and get a result.
Last, it will display the result in the string "The sum is xxx" where xxx is the calculated value.


<HTML>
<head>
   
 <script language="JavaScript">
    function MultiplyNumbers()
    {
      var number1,      // first number to add
      number2,      // second number to add
      product;         // sum of number1 and number2
   
     // convert numbers from strings to integers
      number1 = parseInt(document.frmMultiply.txtfirstNumber.value);
      number2 = parseInt(document.frmMultiply.txtsecondNumber.value);

    // Multiply the numbers
    product = number1 * number2;

   // display the results
      alert( "The product is " + product + " ");
      }
    </script>
    </head>

  <body>

<H1> Welcome to My Web Page</H1>
   Rest of page goes here. This is where you can put pictures and text about yourself and about your project.

<br>

  <form name="frmMultiply">
  Enter first integer: <input type="text" name="txtfirstNumber" /><br />
  Enter second integer: <input type="text" name="txtsecondNumber" /><br>
  <input type="button" value="Multiply" onclick="MultiplyNumbers();">
<p>
</form>             
</body>

</html>

  

<br> 

#### Enhancing the Simple JavaScript program 

 <html>
<head>

<script language="JavaScript">
function MultiplyNumbers()
 {
 var number1, // first number to add
     number2,// second number to add
     product; // product of number1 and number2
 
 // convert numbers from strings to integers
    number1 = parseInt(document.frmMultiply.txtfirstNumber.value);
    number2 = parseInt(document.frmMultiply.txtsecondNumber.value);

  // Multiply the numbers
     product = number1 * number2;

  // display the results
     document.frmMultiply.results.value = product;
}
 </script>

</head>

  <body>
  <form method=post name="frmMultiply">
<table border="1" cellpadding=5>
<tr>
<td align=center>Enter First Integer:</td>
<td align=center><input type="text" name="txtfirstNumber" /></td>
</tr>
<tr>
<td align=center>Enter Second Integer:</td>
<td align=center><input type="text" name="txtsecondNumber" /></td>
</tr>
<tr>
<td align=center><input type="button" value="Multiply" name="multiply" onclick="MultiplyNumbers();"></td>
<td align=center><input type="text" name="results" value=""></td>
</tr
<tr>
 <td colspan="2" align="center"> <input value="Reset" type="reset"></td>
 </tr>

</table>

</form>   

</body>

</html>

 

 

++++++++++++++++++++++++++++++++++++++++++++++++++

 

W3Schools LightBulb Application (Links to an external site.)

 

(Note: Download these lightbulbs images and put them in same folder as web page)

 

<!DOCTYPE html>
<html>
<body>

<h1>What Can JavaScript Do?</h1>

<p>JavaScript can change HTML attributes.</p>

<p>In this case JavaScript changes the src (source) attribute of an image.</p>

<button onclick="document.getElementById('myImage').src='pic_bulbon.gif'">Turn on the light</button>

<img id="myImage" src="pic_bulboff.gif" style="width:100px">

<button onclick="document.getElementById('myImage').src='pic_bulboff.gif'">Turn off the light</button>

</body>
</html>

 

 

JavaScript and Web Mapping Applications

In GIS, we embed interactive maps into web pages, then use JavaScript to pass information to the map. The map responds by carrying out the requests that are passed to it.
