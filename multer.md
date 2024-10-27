1. `multer.diskStorage`
2. Multer Disk Storage Configuration with Error Handling

---

1. `multer.diskStorage`

`multer.diskStorage` ek function hai jo Multer ko batata hai ki uploaded files ko disk (computer storage) pe kaise aur kahan store karna hai. Yeh function do cheezen specify karne ke liye use hota hai:

1. **Destination**: File ko kahan store karna hai.
2. **Filename**: File ka naam kya rakha jayega.

Chaliye isko simple example ke sath samajhte hain:

### Multer Disk Storage Configuration

```javascript
import multer from "multer";

// Disk Storage configuration
const storage = multer.diskStorage({
  // Destination function
  destination: function (req, file, cb) {
    // Specify the folder where files should be saved
    cb(null, "./public/temp");
  },
  // Filename function
  filename: function (req, file, cb) {
    // Specify the name of the file
    cb(null, file.originalname);
  },
});

// Creating the upload middleware
export const upload = multer({ storage });
```

#### Breakdown:

1. **Destination**:

   - `destination` ek function hai jo yeh specify karta hai ki file ko kis folder mein store karna hai.
   - Is function ke parameters mein `req` (request object), `file` (file object), aur `cb` (callback function) hote hain.
   - `cb(null, './public/temp')` yeh callback ko call karta hai aur batata hai ki file `./public/temp` folder mein store ki jayegi. `null` first parameter hai jo error ko represent karta hai (isme koi error nahi hai isliye null).

2. **Filename**:
   - `filename` ek function hai jo yeh specify karta hai ki file ka naam kya hoga.
   - Is function ke parameters mein bhi `req`, `file`, aur `cb` hote hain.
   - `cb(null, file.originalname)` yeh callback ko call karta hai aur file ka original naam set karta hai. `file.originalname` file ka original naam hota hai jab yeh upload hoti hai.

### Usage in Express.js

Multer ko Express.js route mein use karne ke liye, aap `upload` middleware ko use kar sakte hain:

```javascript
import express from "express";
import { upload } from "./path/to/upload";

const app = express();

// Route to handle file upload
app.post("/upload", upload.single("file"), (req, res) => {
  res.send("File uploaded successfully!");
});

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});
```

#### Explanation:

- `upload.single('file')` middleware batata hai ki ek single file upload hogi jiska field name `file` hai.
- Jab client is route pe request bhejta hai (like `POST /upload`), Multer file ko handle karta hai, usse specified destination folder mein save karta hai aur specified filename use karta hai.
- File upload hone ke baad, route handler (callback function) execute hota hai aur response send karta hai.

Is tarah `multer.diskStorage` function use karke, aap upload hone wali files ko disk pe kaise aur kahan store karna hai, yeh specify kar sakte hain.

---

2. Multer Disk Storage Configuration with Error Handling

Agar error ho to `null` ki jagah error ko pass karte hain callback function (`cb`) mein. Yaha pe `null` batata hai ki koi error nahi hai. Agar koi error hoti, to aap error object ko pass karte hain `cb` function ke first argument mein.

Chaliye ek example dekhte hain jisme hum error ko handle karte hain:

### Multer Disk Storage Configuration with Error Handling

```javascript
import multer from "multer";

const storage = multer.diskStorage({
  // Destination function
  destination: function (req, file, cb) {
    // Suppose you want to check some condition before saving the file
    const error = null; // Initially, assume no error

    // Example condition: check if the file type is allowed
    const allowedTypes = ["image/jpeg", "image/png"];
    if (!allowedTypes.includes(file.mimetype)) {
      // If file type is not allowed, create an error
      error = new Error("Invalid file type");
    }

    // Call the callback with error (if any) and destination path
    cb(error, "./public/temp");
  },
  // Filename function
  filename: function (req, file, cb) {
    // Example condition: check if the file name is appropriate
    const error = null; // Initially, assume no error

    // Check if the file name has prohibited characters or length
    if (file.originalname.length > 100) {
      // If file name is too long, create an error
      error = new Error("File name is too long");
    }

    // Call the callback with error (if any) and the file name
    cb(error, file.originalname);
  },
});

// Creating the upload middleware
export const upload = multer({ storage });
```

### Usage in Express.js with Error Handling

```javascript
import express from "express";
import { upload } from "./path/to/upload";

const app = express();

// Route to handle file upload
app.post("/upload", (req, res, next) => {
  upload.single("file")(req, res, function (err) {
    if (err) {
      // Handle Multer-specific errors
      return res.status(400).send(err.message);
    }
    // Handle success
    res.send("File uploaded successfully!");
  });
});

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});
```

#### Explanation:

1. **Destination Function**:

   - `const error = null;` initially assume karte hain ki koi error nahi hai.
   - Check karte hain agar file type allowed hai ya nahi (`allowedTypes.includes(file.mimetype)`). Agar allowed types mein file type nahi hai, to `error = new Error('Invalid file type');` set karte hain.
   - `cb(error, './public/temp')` callback ko call karte hain error (agar koi hai to) aur destination path ke sath.

2. **Filename Function**:

   - Similarly, check karte hain agar file name appropriate hai. Example mein file name ki length check karte hain.
   - Agar file name bahut lamba hai, to `error = new Error('File name is too long');` set karte hain.
   - `cb(error, file.originalname)` callback ko call karte hain error (agar koi hai to) aur file name ke sath.

3. **Route Handling in Express**:
   - `upload.single('file')(req, res, function (err) {...})` use karte hain to handle the file upload.
   - Agar koi error hoti hai during the file upload, to `err` parameter set hota hai. Is case mein, response mein error message bhejte hain (`res.status(400).send(err.message);`).
   - Agar koi error nahi hoti, to success message bhejte hain (`res.send('File uploaded successfully!');`).

Is tarah aap errors ko handle kar sakte hain aur ensure kar sakte hain ki upload hone wali files appropriate checks pass kar rahi hain.
