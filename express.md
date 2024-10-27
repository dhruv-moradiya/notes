1. app.use(express.json({ limit: "16kb" }))
2. app.use(express.urlencoded({ extended: true, limit: "16kb" }))

---

1. app.use(express.json({ limit: "16kb" }))

`app.use(express.json({ limit: "16kb" }))` middleware ka use tab hota hai jab aapka server incoming HTTP requests handle kar raha hota hai jinki body JSON format me hoti hai. Yahaan kuch scenarios diye gaye hain jahan yeh middleware useful hoga:

### Scenarios for Using `app.use(express.json({ limit: "16kb" }))`

1. **Client Request Sending JSON Data:**
   Jab client (browser, mobile app, etc.) JSON data ke sath POST, PUT, ya PATCH request bhejta hai, tab yeh middleware us JSON data ko parse karega taaki aapka server us data ko access aur process kar sake.

   ```javascript
   // Client sending JSON data in a POST request
   fetch("http://localhost:8000/api/v1/users", {
     method: "POST",
     headers: {
       "Content-Type": "application/json",
     },
     body: JSON.stringify({
       username: "john_doe",
       password: "12345",
     }),
   });
   ```

2. **API Handling JSON Data:**
   Jab aap RESTful API bana rahe hain jaha endpoints JSON data receive karte hain, tab yeh middleware zaroori hai. Yeh parsed JSON data ko `req.body` property me store karega taaki aap usse aage process kar sake.

   ```javascript
   app.post("/api/v1/users", (req, res) => {
     const { username, password } = req.body;
     // Process the data
     res.send("User registered successfully");
   });
   ```

### Explanation of Middleware

- **Request Parsing:**
  Jab bhi server ko koi HTTP request milti hai jisme `Content-Type: application/json` hota hai, yeh middleware us request body ko parse karta hai aur JSON object me convert karta hai. Yeh object `req.body` property me store hota hai.

- **Size Limit:**
  `limit: "16kb"` ka matlab hai ki server maximum 16KB size ka JSON data accept karega. Agar request body 16KB se zyada badi hoti hai, toh server request ko reject kar dega aur 413 Payload Too Large status code return karega.

### Example with Middleware

```javascript
app.post("/api/v1/users", (req, res) => {
  const { username, password } = req.body;
  console.log("Received data:", req.body);

  // Example response
  res.status(200).json({
    message: "User data received successfully",
    user: { username, password },
  });
});
```

Is example me, jab client `/api/v1/users` endpoint par POST request bhejta hai, to yeh middleware us JSON body ko parse karega, aur aap us parsed data ko `req.body` me access kar sakte hain aur use process kar sakte hain.

### Summary

`app.use(express.json({ limit: "16kb" }))` tab use hota hai jab aapko server par incoming JSON payloads ko handle karna hota hai. Yeh middleware ensure karta hai ki aapka server JSON data ko sahi se parse kar sake aur size limits enforce kare, taaki large payloads server ki performance ko impact na kar sake.

---

2. app.use(express.urlencoded({ extended: true, limit: "16kb" }))

`app.use(express.urlencoded({ extended: true, limit: "16kb" }))` middleware ka use tab hota hai jab aapka server incoming HTTP requests handle kar raha hota hai jinki body URL-encoded format me hoti hai. URL-encoded data aksar HTML forms se aata hai. Yahaan kuch scenarios diye gaye hain jahan yeh middleware useful hoga:

### Scenarios for Using `app.use(express.urlencoded({ extended: true, limit: "16kb" }))`

1. **HTML Forms Data Submission:**
   Jab client (browser) HTML form submit karta hai aur data URL-encoded format me bhejta hai (default form submission format), tab yeh middleware us data ko parse karega.

   ```html
   <!-- HTML form example -->
   <form action="/api/v1/users" method="post">
     <label for="username">Username:</label>
     <input type="text" id="username" name="username" />
     <label for="password">Password:</label>
     <input type="password" id="password" name="password" />
     <button type="submit">Submit</button>
   </form>
   ```

   Jab yeh form submit hota hai, toh data URL-encoded format me bheja jata hai, jise yeh middleware parse karega.

2. **API Handling Form Data:**
   Jab aapke RESTful API endpoints ko URL-encoded data receive karna hota hai, tab yeh middleware zaroori hai. Yeh parsed URL-encoded data ko `req.body` property me store karega taaki aap us data ko access aur process kar sake.

   ```javascript
   app.post("/api/v1/users", (req, res) => {
     const { username, password } = req.body;
     // Process the data
     res.send("User registered successfully");
   });
   ```

### Explanation of Middleware

- **Request Parsing:**
  Jab bhi server ko koi HTTP request milti hai jisme `Content-Type: application/x-www-form-urlencoded` hota hai, yeh middleware us request body ko parse karta hai aur URL-encoded data ko JavaScript object me convert karta hai. Yeh object `req.body` property me store hota hai.

- **Extended Option:**
  `extended: true` ka matlab hai ki yeh middleware nested objects ko bhi parse kar sakta hai. Agar aap `extended: false` set karte hain, toh yeh sirf simple key-value pairs ko parse karega.

- **Size Limit:**
  `limit: "16kb"` ka matlab hai ki server maximum 16KB size ka URL-encoded data accept karega. Agar request body 16KB se zyada badi hoti hai, toh server request ko reject kar dega aur 413 Payload Too Large status code return karega.

### Example with Middleware

```javascript
app.post("/api/v1/users", (req, res) => {
  const { username, password } = req.body;
  console.log("Received data:", req.body);

  // Example response
  res.status(200).json({
    message: "User data received successfully",
    user: { username, password },
  });
});
```

Is example me, jab client `/api/v1/users` endpoint par POST request URL-encoded data ke sath bhejta hai, to yeh middleware us data ko parse karega, aur aap us parsed data ko `req.body` me access kar sakte hain aur use process kar sakte hain.

### Summary

`app.use(express.urlencoded({ extended: true, limit: "16kb" }))` tab use hota hai jab aapko server par incoming URL-encoded payloads ko handle karna hota hai. Yeh middleware ensure karta hai ki aapka server URL-encoded data ko sahi se parse kar sake aur size limits enforce kare, taaki large payloads server ki performance ko impact na kar sake.
