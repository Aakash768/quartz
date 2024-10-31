### **What is Form Handling?**

Form handling is the process of managing and processing data submitted through HTML forms in a web application. It involves receiving, validating, and storing the data submitted by users through forms, such as login credentials, registration information, or feedback.

**Express** allows you to easily handle form submissions, especially when combined with middleware like `express.urlencoded()` to parse form data.

#### Steps:

1. **Parse Form Data**: To process form submissions, add middleware to parse URL-encoded data.
    ```js
    app.use(express.urlencoded({ extended: true }));
    //or
    app.use(express.json());
```

2. **Define Form Route (GET)**: Serve a form with a `GET` request.
	```js
	app.get('/form', (req, res) => {   
	res.send(
	<form action="/submit" method="POST">       
	<input type="text" name="username" placeholder="Enter username" required>    <button type="submit">Submit</button>     
	</form>); 
	})
	```
	
	OR
	
	Create a HTML File
	```html
		<!DOCTYPE html>
		<html>
		<head>
		  <title>Form Example</title>
		</head>
		<body>
		  <h1>Form Example</h1>
		  <form action="/submit" method="post">
		    <label for="name">Name:</label>
		    <input type="text" id="name" name="name"><br><br>
		    <label for="email">Email:</label>
		    <input type="email" id="email" name="email"><br><br>
		    <label for="message">Message:</label>
		    <textarea id="message" name="message"></textarea><br><br>
		    <input type="submit" value="Submit">
		  </form>
		</body>
		</html>
```

	Link this HTML to Node.js (Script.js)
	```js
		const path = require("path");
		
		app.get("/", (req, res) => {
		res.sendFile(__dirname + "/index.html");  //path of your index.html
		});			```

3. **Handle Form Submission (POST)**: Process the form data in the route defined by `action`.
	```js
	const express = require("express");
	const app = express();
	const path = require("path");
	  
	
	app.use(express.urlencoded({ extended: true }))
	
	app.get("/", (req, res) => {
	    res.sendFile(__dirname + "/index.html");
	});
	  
	app.post("/submit", (req, res) => {
	    const data = req.body;
	    console.log(data);
	    res.send("Form submitted Successful");
	})  
	
	app.listen(3000, () => {
	    console.log("listening on port 3000")
	})
	```