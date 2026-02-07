type:: Permanent
tags:: #Textbox, #GUI, #JavaScript
references:: [W3Schools CreateElement](https://www.w3schools.com/jsref/met_document_createelement.asp), [W3Schools HTML Input types](https://www.w3schools.com/html/html_form_input_types.asp)

-
-
-
- ```JavaScript
  <h1>Create a textbox with JavaScript</h1>
  <br>
  
  
  <script>
  
      document.body.appendChild(document.createElement("br"));
      const tb1 = document.createElement("input")
      tb1.name = "Textbox1"
      tb1.id = "Textbox1"
      tb1.placeholder = "Interactive text box"
      document.body.appendChild(tb1);
      document.body.appendChild(document.createElement("br"));
  
  </script>
  
  
  <script>
  
      function getInputValue() {
          // Select the element by its ID and get the value
          var inputVal = document.getElementById("Textbox1").value;
          alert("You typed: " + inputVal);
      }
  
  
  </script>
  
  <br>
  <button onclick="getInputValue()">Submit</button>
  ```