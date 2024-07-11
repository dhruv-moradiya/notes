## JAVASCRIPT

1. What is event bubbling in js ?

- Event bubbling is a concept in JavaScript where an event starts from the deepest target element and then bubbles up to the ancestor elements in the DOM tree. When an event occurs on an element, it first triggers the event handlers on the target element, and then it moves up to the parent element, and so on, until it reaches the document object.

  1. Target Phase:
     - The event is dispatched to the target element where it originated.
  2. Bubbling Phase:
     - After reaching the target element, the event bubbles up through its ancestors. This means the event is passed to each parent node sequentially, triggering any event handlers set for that specific event type along the way.

### Example

```HTML
<div id="grandparent">
  <div id="parent">
    <button id="child">Click Me</button>
  </div>
</div>
```

```js
document.getElementById("grandparent").addEventListener("click", () => {
  console.log("Grandparent clicked");
});

document.getElementById("parent").addEventListener("click", () => {
  console.log("Parent clicked");
});

document.getElementById("child").addEventListener("click", () => {
  console.log("Child clicked");
});
```

When the button with the id child is clicked, the output will be:

      - Child clicked
      - Parent clicked
      - Grandparent clicked

- This output demonstrates the bubbling phase: the event triggers the child's click event, then it bubbles up to the parent, and finally to the grandparent.

- Stopping Event Bubbling
  - To stop an event from bubbling up the DOM tree, you can use the event.stopPropagation() method. Here is how you can modify the previous example to stop the event bubbling:

```js
document.getElementById("child").addEventListener("click", (event) => {
  event.stopPropagation();
  console.log("Child clicked");
});
```

---

2. Event Capturing

- Event capturing is the opposite of event bubbling. It starts from the document and propagates down to the target element. To use event capturing, you can set the third parameter of addEventListener to true:

```js
document.getElementById("grandparent").addEventListener(
  "click",
  () => {
    console.log("Grandparent clicked");
  },
  true
);

document.getElementById("parent").addEventListener(
  "click",
  () => {
    console.log("Parent clicked");
  },
  true
);

document.getElementById("child").addEventListener(
  "click",
  () => {
    console.log("Child clicked");
  },
  true
);
```

- When you click the child button with event capturing, the output will be:
  - Grandparent clicked
  - Parent clicked
  - Child clicked

---

3.  what is promise and how it is work ?

    - A Promise in JavaScript is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. It allows you to write asynchronous code in a more synchronous and readable manner. Promises are part of modern JavaScript and are fundamental for handling asynchronous operations such as network requests, file operations, or timed events.

    #### States of a Promise

    - Pending: The initial state. The operation is ongoing and neither fulfilled nor rejected.
    - Fulfilled: The operation completed successfully. The promise has a resulting value.
    - Rejected: The operation failed. The promise has a reason for the failure (an error).

    #### How Promises Work

    - A Promise is created using the Promise constructor, which takes a function (known as the executor function) with two parameters: resolve and reject. These are functions that you call to transition the Promise from the pending state to fulfilled or rejected.

    ```js
    // Create a new Promise
    let myPromise = new Promise((resolve, reject) => {
      let success = true; // Simulate a condition

      if (success) {
        resolve("Operation was successful!"); // Transition to fulfilled
      } else {
        reject("Operation failed!"); // Transition to rejected
      }
    });
    // Consume the Promise
    myPromise
      .then((result) => {
        console.log(result); // "Operation was successful!"
      })
      .catch((error) => {
        console.log(error); // If it was rejected, log the error message
      });
    ```

    #### Using Promises

    1. then(): Attaches callbacks for the fulfillment and rejection cases.
    2. catch(): Attaches a callback for only the rejection case.
    3. finally(): Attaches a callback that will be executed regardless of the promise's outcome (either fulfilled or rejected).

---

4.  what is callback hell in js ?

        - Callback hell in JavaScript refers to a situation where multiple nested callbacks are used to handle asynchronous operations. This nesting can make the code difficult to read, maintain, and debug. It often occurs when you have several asynchronous tasks that need to be executed in sequence or when one asynchronous task depends on the results of another.

    ```js
    fetchRandomJoke((joke) => {
      console.log(joke);

      translateJoke(joke, (translatedJoke) => {
        console.log(translatedJoke);

        postJoke(translatedJoke, () => {
          console.log("Joke posted successfully!");
        });
      });
    });
    ```

    #### Avoiding Callback Hell

    1. Modularize Callbacks: Break down the nested callbacks into separate functions.
    2. Promises: Use Promises to handle asynchronous operations in a more readable way.
    3. Async/Await: Use async and await to write asynchronous code that looks synchronous.

5.  Difference between `.then()/.catch()` and `async/await` ?

- The primary difference between `.then()/.catch()` and `async/await` in JavaScript lies in how they handle asynchronous operations and improve code readability.

### `.then()/.catch()`

#### Advantages:

- Chaining: You can chain multiple asynchronous operations.
  Error Handling: Errors can be caught using .catch() at the end of the chain.

#### Disadvantages:

- Readability: When dealing with multiple asynchronous operations, chaining can become complex and less readable, especially with nested .then() calls.

### `async/await`

- async and await are syntactic sugar built on top of Promises, introduced in ES2017, to write asynchronous code that looks synchronous.

#### Advantages:

- Readability: Code looks more like synchronous code, making it easier to read and understand.
- Error Handling: Using try/catch blocks for error handling makes the structure similar to synchronous code.

#### Disadvantages:

- Browser Compatibility: While widely supported, very old browsers might not support async/await without polyfills.
- Must be inside an async function: You can only use await inside an async function.

---

5. Class

- in JavaScript, a class is a blueprint for creating objects with shared properties and methods. Classes are part of the ECMAScript 6 (ES6) standard

#### Basic Syntax

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}

const person1 = new Person("Alice", 30);
person1.greet(); // Output: Hello, my name is Alice and I am 30 years old.
```

#### Constructor

- In JavaScript, a constructor is a special method of a class that is used to initialize objects created from that class. The constructor method is called automatically when a new instance of the class is created. It is typically used to set up initial values for the properties of the object

#### Inheritance

- Classes in JavaScript can inherit from other classes using the extends keyword. The super keyword is used to call the constructor of the parent class.

```js
class Employee extends Person {
  constructor(name, age, jobTitle) {
    super(name, age); // calls the constructor of the parent class
    this.jobTitle = jobTitle;
  }

  work() {
    console.log(`${this.name} is working as a ${this.jobTitle}.`);
  }
}

const employee1 = new Employee("Bob", 25, "Developer");
employee1.greet(); // Output: Hello, my name is Bob and I am 25 years old.
employee1.work(); // Output: Bob is working as a Developer.
```

#### Private Fields and Methods

- As of ECMAScript 2022, JavaScript supports private fields and methods, which are prefixed with a #. These members are only accessible within the class.

```js
class BankAccount {
  #balance;

  constructor(initialBalance) {
    this.#balance = initialBalance;
  }

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount(1000);
account.deposit(500);
console.log(account.getBalance()); // Output: 1500
console.log(account.#balance); // SyntaxError: Private field '#balance' must be declared in an enclosing class
```

- Classes in JavaScript provide a clear and concise way to create objects and handle inheritance. They make the code more readable and maintainable by encapsulating related data and functionality within a single construct. Despite being syntactic sugar over the existing prototypical inheritance, they align JavaScript more closely with class-based programming languages, making it easier for developers from those backgrounds to adapt.

---

6. Static Method

In JavaScript, the `static` keyword is used to define static methods and properties for a class. Static methods and properties are not called on instances of the class but rather on the class itself. They are useful for utility functions, constants, or any functionality that doesn't require an instance of the class to operate.

### Key Features of `static`:

1. **Class-Level Methods and Properties:**

   - Static methods and properties belong to the class itself rather than any instance of the class.

2. **Accessed on the Class:**

   - They are called directly on the class and cannot be called on instances of the class.

3. **Shared Across Instances:**
   - Static members are shared across all instances of the class. There is only one copy of each static member, regardless of how many instances of the class are created.

### Syntax:

To define a static method or property, you use the `static` keyword followed by the method or property name.

### Static Methods:

```javascript
class MathHelper {
  static square(number) {
    return number * number;
  }

  static cube(number) {
    return number * number * number;
  }
}

console.log(MathHelper.square(4)); // Output: 16
console.log(MathHelper.cube(3)); // Output: 27
```

In this example, `square` and `cube` are static methods of the `MathHelper` class. They are called on the class itself (`MathHelper.square(4)`), not on an instance of the class.

### Static Properties:

```javascript
class Config {
  static apiUrl = "https://api.example.com";
  static timeout = 5000;
}

console.log(Config.apiUrl); // Output: https://api.example.com
console.log(Config.timeout); // Output: 5000
```

Here, `apiUrl` and `timeout` are static properties of the `Config` class. They are accessed directly on the class (`Config.apiUrl`).

### Example with Both Static Methods and Properties:

```javascript
class Calculator {
  static pi = 3.14159;

  static calculateCircumference(radius) {
    return 2 * Calculator.pi * radius;
  }
}

console.log(Calculator.pi); // Output: 3.14159
console.log(Calculator.calculateCircumference(10)); // Output: 62.8318
```

In this example, `pi` is a static property, and `calculateCircumference` is a static method of the `Calculator` class. Both are accessed on the class itself.

### Using Static Members in Inheritance:

Static members can also be inherited by subclasses. Here's an example:

```javascript
class ParentClass {
  static staticMethod() {
    return "Parent static method";
  }
}

class ChildClass extends ParentClass {}

console.log(ChildClass.staticMethod()); // Output: Parent static method
```

In this example, `ChildClass` inherits the static method `staticMethod` from `ParentClass`.

### Summary:

- **Static Methods:** Defined using the `static` keyword. Called on the class itself, not on instances.
- **Static Properties:** Also defined using the `static` keyword. Accessed on the class itself.
- **Inheritance:** Static members can be inherited by subclasses.

Static members are a powerful feature in JavaScript, allowing you to define functionality and data that are relevant to the class as a whole, rather than to any specific instance.

---

7. mutating methods and non - mutating methods in js

### Mutating Methods

These methods change the original array or object.

| Method                      | Description                                                           |
| --------------------------- | --------------------------------------------------------------------- |
| `push()`                    | Adds one or more elements to the end of an array.                     |
| `pop()`                     | Removes the last element from an array.                               |
| `shift()`                   | Removes the first element from an array.                              |
| `unshift()`                 | Adds one or more elements to the beginning of an array.               |
| `splice()`                  | Adds or removes elements from an array.                               |
| `sort()`                    | Sorts the elements of an array in place and returns the array.        |
| `reverse()`                 | Reverses the order of the elements in an array in place.              |
| `fill()`                    | Fills elements of an array with a static value.                       |
| `copyWithin()`              | Copies part of an array to another location in the same array.        |
| `Array.prototype.set`       | Changes the values of elements in an array-like object.               |
| `Object.assign()`           | Copies properties from one or more source objects to a target object. |
| `Object.defineProperty()`   | Adds or modifies properties directly on an object.                    |
| `Object.defineProperties()` | Adds or modifies multiple properties directly on an object.           |

### Non-Mutating Methods

These methods do not change the original array or object but return a new array or value.

| Method             | Description                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| `concat()`         | Merges two or more arrays.                                                                                        |
| `slice()`          | Returns a shallow copy of a portion of an array.                                                                  |
| `map()`            | Creates a new array with the results of calling a provided function on every element in the calling array.        |
| `filter()`         | Creates a new array with all elements that pass the test implemented by the provided function.                    |
| `reduce()`         | Executes a reducer function on each element of the array, resulting in a single output value.                     |
| `reduceRight()`    | Executes a reducer function on each element of the array, from right to left, resulting in a single output value. |
| `flatMap()`        | Maps each element using a mapping function, then flattens the result into a new array.                            |
| `flat()`           | Creates a new array with all sub-array elements concatenated into it recursively up to the specified depth.       |
| `join()`           | Joins all elements of an array into a string.                                                                     |
| `every()`          | Tests whether all elements in the array pass the test implemented by the provided function.                       |
| `some()`           | Tests whether at least one element in the array passes the test implemented by the provided function.             |
| `find()`           | Returns the value of the first element in the array that satisfies the provided testing function.                 |
| `findIndex()`      | Returns the index of the first element in the array that satisfies the provided testing function.                 |
| `includes()`       | Determines whether an array includes a certain value among its entries.                                           |
| `indexOf()`        | Returns the first index at which a given element can be found in the array.                                       |
| `lastIndexOf()`    | Returns the last index at which a given element can be found in the array.                                        |
| `Array.from()`     | Creates a new, shallow-copied Array instance from an array-like or iterable object.                               |
| `Array.of()`       | Creates a new Array instance with a variable number of arguments, regardless of number or type of the arguments.  |
| `Object.keys()`    | Returns an array of a given object's own enumerable property names.                                               |
| `Object.values()`  | Returns an array of a given object's own enumerable property values.                                              |
| `Object.entries()` | Returns an array of a given object's own enumerable string-keyed property `[key, value]` pairs.                   |
| `Object.freeze()`  | Freezes an object: other code cannot delete or change its properties.                                             |
| `Object.seal()`    | Prevents new properties from being added to an object, but allows the modification of existing properties.        |

This table includes both array and object methods, covering a broad range of common use cases in JavaScript development.

---

8. Server-Side Rendering and Client-Side Rendering

**Server-Side Rendering (SSR):**

- Server-side rendering mein, jab aap ek webpage ko open karte ho, toh saari processing aur rendering server pe hoti hai. Matlab, server HTML page ko generate karta hai aur usko browser ko bhejta hai. Jab browser ko page milta hai, tab woh usko directly display kar sakta hai. Ye process thoda slow ho sakta hai kyunki har request pe server ko poora page generate karna padta hai. Par iska fayda ye hai ki SEO (Search Engine Optimization) better hota hai aur initial load time fast hota hai.

**Pros:**

1. **SEO Friendly:**

   - SSR pages ko search engines easily crawl kar sakte hain kyunki content already HTML mein present hota hai.

2. **Fast Initial Load:**

   - Jab user pehli baar page open karta hai, to content jaldi load hota hai because server se complete HTML milta hai.

3. **Better for Static Content:**

   - Static content ya rarely changing content ke liye SSR best hota hai kyunki server se har request par same HTML bheja ja sakta hai.

4. **Compatible with Older Browsers:**
   - SSR pages older browsers pe bhi easily render ho jaate hain kyunki unhe sirf HTML display karna hota hai.

**Cons:**

1. **Server Load:**

   - Har request pe server ko poora page generate karna padta hai, which increases server load, especially for dynamic content.

2. **Slower Interactivity:**

   - Page load hone ke baad bhi, kuch interactive elements ko load hone mein time lag sakta hai jab tak poora content server se nahi aa jaata.

3. **Scalability Issues:**
   - Bahut saari concurrent requests handle karne mein problems ho sakti hain, leading to slower response times under heavy load.

**Client-Side Rendering (CSR):**

- Client-side rendering mein, jab aap webpage ko open karte ho, toh server sirf ek basic HTML file bhejta hai aur saara JavaScript code. Browser pe JavaScript run hota hai aur wahi dynamically HTML content generate karta hai aur display karta hai. Iska fayda ye hai ki once initial load ho gaya, subsequent interactions fast hote hain. Par initial load thoda slow ho sakta hai aur SEO ke liye thoda mushkil hota hai, kyunki search engines ko page ka content directly nahi milta, unhe JavaScript execute karna padta hai.

**Pros:**

1. **Rich Interactivity:**

   - CSR pages bahut zyada interactive ho sakte hain because JavaScript dynamically update kar sakta hai content bina poora page reload kiye.

2. **Reduced Server Load:**

   - Server ko sirf basic HTML aur JavaScript file bhejni hoti hai, baaki processing client-side pe hoti hai, which reduces server load.

3. **Smooth User Experience:**

   - Once initial load ho jata hai, further interactions fast aur seamless hote hain because content dynamically load hota hai.

4. **Efficient for SPAs:**
   - Single Page Applications (SPAs) ke liye CSR ideal hota hai because page ke different parts ko bina reload kiye update kar sakte hain.

**Cons:**

1. **SEO Challenges:**

   - CSR pages ko search engines crawl karne mein problem hoti hai because content dynamically generate hota hai, jo har crawler easily nahi handle kar sakta.

2. **Slower Initial Load:**

   - Initial page load thoda slow ho sakta hai because browser ko JavaScript execute karna padta hai to render the content.

3. **JavaScript Dependency:**

   - JavaScript disable hone par ya slow internet connection pe, CSR pages properly render nahi hote.

4. **Complexity:**
   - Development aur debugging CSR applications kaafi complex ho sakti hai compared to SSR applications.

**Example:**

1. **Server-Side Rendering:**

   - Request: User ne URL type kiya aur enter press kiya.
   - Server: Server ne HTML page generate kiya aur browser ko bheja.
   - Browser: Browser ne page display kar diya.

2. **Client-Side Rendering:**
   - Request: User ne URL type kiya aur enter press kiya.
   - Server: Server ne basic HTML aur JavaScript bheja.
   - Browser: Browser ne JavaScript execute karke content generate kiya aur display kiya.

---

9. var, let, const

### `var` Keyword

1. **Function Scope:**

   - `var` ka scope sirf us function tak hota hai jismein woh declare hua hai. Agar function ke bahar declare hota hai, toh woh global scope mein hota hai.
   - Example:
     ```javascript
     function example() {
       var x = 10;
       if (true) {
         var y = 20;
         console.log(x); // 10
         console.log(y); // 20
       }
       console.log(y); // 20 (still accessible)
     }
     console.log(x); // Error: x is not defined
     ```

2. **Hoisting:**

   - `var` variables hoist hote hain, matlab declaration code ke top pe move ho jati hai, lekin unki initialization wahi rehti hai.
   - Example:
     ```javascript
     console.log(a); // undefined
     var a = 5;
     ```

3. **Re-declaration:**
   - `var` ko same scope mein multiple times re-declare kiya ja sakta hai bina kisi error ke.
   - Example:
     ```javascript
     var b = 10;
     var b = 20; // No error
     console.log(b); // 20
     ```

### `let` Keyword

1. **Block Scope:**

   - `let` ka scope sirf us block tak hota hai jismein woh declare hota hai, jaise `{}` ke andar.
   - Example:
     ```javascript
     function example() {
       let x = 10;
       if (true) {
         let y = 20;
         console.log(x); // 10
         console.log(y); // 20
       }
       console.log(y); // Error: y is not defined
     }
     ```

2. **Hoisting:**

   - `let` variables bhi hoist hote hain, lekin unko initialize nahi kiya jata. They remain in a "temporal dead zone" until the declaration line.
   - Example:
     ```javascript
     console.log(a); // Error: Cannot access 'a' before initialization
     let a = 5;
     ```

3. **No Re-declaration:**
   - `let` ko same scope mein dobara declare nahi kiya ja sakta. It will throw an error.
   - Example:
     ```javascript
     let b = 10;
     let b = 20; // Error: Identifier 'b' has already been declared
     ```

**Summary:**

- `var` function-scoped hota hai aur hoisting ke saath initialized hota hai as `undefined`. Re-declaration allowed hai.
- `let` block-scoped hota hai aur temporal dead zone mein rehta hai jab tak uski declaration nahi hoti. Re-declaration allowed nahi hai.

### `const` Keyword

1. **Block Scope:**

   - `const` ka scope bhi `let` ki tarah block-scoped hota hai. Matlab, `const` sirf us block `{}` ke andar accessible hota hai jahan usko declare kiya gaya hai.
   - Example:
     ```javascript
     function example() {
       const x = 10;
       if (true) {
         const y = 20;
         console.log(x); // 10
         console.log(y); // 20
       }
       console.log(y); // Error: y is not defined
     }
     ```

2. **Hoisting:**

   - `const` variables bhi hoist hote hain, lekin initialization nahi hoti until the declaration line. They remain in a "temporal dead zone" until the declaration.
   - Example:
     ```javascript
     console.log(a); // Error: Cannot access 'a' before initialization
     const a = 5;
     ```

3. **Immutable Binding:**

   - `const` ka use jab aap karte ho, tab us variable ko re-assign nahi kar sakte. However, agar `const` object ya array ko point kar raha hai, toh aap us object ke properties ya array ke elements ko modify kar sakte ho.
   - Example:

     ```javascript
     const b = 10;
     b = 20; // Error: Assignment to constant variable

     const obj = { name: "John" };
     obj.name = "Doe"; // Allowed
     console.log(obj.name); // Doe

     const arr = [1, 2, 3];
     arr.push(4); // Allowed
     console.log(arr); // [1, 2, 3, 4]
     ```

4. **No Re-declaration:**
   - `const` ko same scope mein dobara declare nahi kiya ja sakta. Yeh `let` ki tarah behave karta hai is aspect mein.
   - Example:
     ```javascript
     const c = 10;
     const c = 20; // Error: Identifier 'c' has already been declared
     ```

### Comparison Summary:

- **Scope:**

  - `var` function-scoped hota hai.
  - `let` aur `const` block-scoped hote hain.

- **Hoisting:**

  - `var` hoist hota hai aur `undefined` se initialized hota hai.
  - `let` aur `const` bhi hoist hote hain, par temporal dead zone mein rehte hain jab tak declare nahi hote.

- **Re-declaration:**

  - `var` ko same scope mein dobara declare kar sakte hain.
  - `let` aur `const` ko same scope mein dobara declare nahi kar sakte.

- **Re-assignment:**
  - `var` aur `let` ko re-assign kar sakte hain.
  - `const` ko re-assign nahi kar sakte, lekin agar `const` object ya array ko point kar raha hai, toh unke contents modify kar sakte hain.

---

10. what is fetch ?

### `fetch` in JavaScript

**Kya Hai?**
`fetch` ek JavaScript function hai jo browser ke andar network requests banane ke liye use hota hai. Yeh asynchronous hota hai, matlab yeh background mein run karta hai aur baki code ko block nahi karta.

**Use Karne Ka Tarika:**
`fetch` function ko aap kisi URL ko request bhejne ke liye use kar sakte ho. Yeh ek promise return karta hai, jo response aane ke baad resolve hota hai.

### Basic Syntax:

```javascript
fetch("URL")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

**Explanation:**

1. **`fetch('URL')`**:

   - Yeh `fetch` function ko call karta hai aur given URL pe request bhejta hai.
   - Ek promise return hota hai jo response object ko represent karta hai.

2. **`.then(response => response.json())`**:

   - Jab response milta hai, tab `.then()` method usko handle karta hai.
   - `response.json()` method response ko JSON format mein convert karta hai.
   - Yeh bhi ek promise return karta hai jo actual data ko represent karta hai.

3. **`.then(data => console.log(data))`**:

   - Next `.then()` method us data ko handle karta hai jo JSON mein convert ho chuka hai.
   - `console.log(data)` data ko console mein print karta hai.

4. **`.catch(error => console.error('Error:', error))`**:
   - Agar kisi bhi step mein koi error aati hai, toh `.catch()` method us error ko handle karta hai aur console mein print karta hai.

### Example:

**Get Request:**

```javascript
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => {
    console.log("Data:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

**Post Request:**

```javascript
fetch("https://api.example.com/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "John",
    age: 30,
  }),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

### Summary:

- `fetch` function asynchronous network requests banane ke liye use hota hai.
- Yeh promises use karta hai to handle response aur errors.
- Simple syntax aur flexibility ki wajah se yeh modern web applications mein kaafi popular hai.

---

11. What is promise.all ?

### `Promise.all` in JavaScript

**Kya Hai?**
`Promise.all` ek method hai jo ek array of promises ko handle karne ke liye use hota hai. Yeh method tab resolve hota hai jab saare promises resolve ho jaate hain, ya phir agar koi ek promise reject ho jata hai, toh yeh method turant reject ho jata hai.

### Basic Syntax:

```javascript
Promise.all([promise1, promise2, promise3])
  .then((results) => {
    // Saare promises resolve hone ke baad yeh execute hoga
    console.log(results); // Array of results
  })
  .catch((error) => {
    // Agar koi bhi promise reject hota hai, toh yeh execute hoga
    console.error("Error:", error);
  });
```

**Explanation:**

1. **`Promise.all([promise1, promise2, promise3])`**:

   - Yeh `Promise.all` method ko call karta hai aur ek array of promises leta hai.
   - `Promise.all` ek promise return karta hai jo resolve hota hai jab saare input promises resolve ho jaate hain.

2. **`.then(results => { ... })`**:

   - Jab saare promises resolve ho jaate hain, toh `.then()` method execute hota hai.
   - `results` ek array hota hai jo saare resolved values ko contain karta hai.

3. **`.catch(error => { ... })`**:
   - Agar input promises mein se koi bhi promise reject hota hai, toh `.catch()` method execute hota hai.
   - `error` woh reason hota hai jiski wajah se koi promise reject hua hai.

### Example:

**Multiple API Requests:**

```javascript
const promise1 = fetch("https://api.example.com/data1").then((response) =>
  response.json()
);
const promise2 = fetch("https://api.example.com/data2").then((response) =>
  response.json()
);
const promise3 = fetch("https://api.example.com/data3").then((response) =>
  response.json()
);

Promise.all([promise1, promise2, promise3])
  .then((results) => {
    // Saare API responses aa gaye
    console.log("Data1:", results[0]);
    console.log("Data2:", results[1]);
    console.log("Data3:", results[2]);
  })
  .catch((error) => {
    // Agar koi bhi request fail ho gayi
    console.error("Error:", error);
  });
```

**Summary:**

- **Saare Promises Complete:** `Promise.all` tab tak wait karta hai jab tak saare promises complete nahi ho jaate. Agar saare promises resolve ho gaye, toh `.then()` execute hota hai aur resolved values ka array milta hai.
- **Koi Ek Fail Hua Toh Fail Sab:** Agar input array mein koi bhi ek promise reject hota hai, toh `Promise.all` turant reject ho jata hai aur `.catch()` execute hota hai.
- **Use Cases:** Ek se zyada asynchronous operations ko parallel mein execute karne ke liye useful hai, jaise multiple API calls.

---

12. Callback

A callback in JavaScript is a function that is passed as an argument to another function and is executed after some operation has been completed. Callbacks are used to handle asynchronous operations, like fetching data from a server, reading files, or waiting for user input.

### How Callbacks Work

1. **Passing a Function as an Argument**: You define a function and pass it as an argument to another function.
2. **Execution After Completion**: The receiving function (the one that takes the callback as an argument) will execute the callback function at a specific point, usually after an asynchronous operation is done.

### Example

Let's look at a simple example to illustrate how callbacks work:

#### Synchronous Example

```javascript
function greet(name) {
  console.log("Hello, " + name);
}

function processUserInput(callback) {
  const name = "John";
  callback(name);
}

processUserInput(greet);
```

- Here, `greet` is a function that takes a name and logs a greeting.
- `processUserInput` is a function that takes a callback function as an argument.
- When `processUserInput(greet)` is called, it executes the `greet` function, passing 'John' as an argument. The output will be `Hello, John`.

#### Asynchronous Example

Callbacks are particularly useful for asynchronous operations like fetching data from a server:

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const data = { name: "John", age: 30 };
    callback(data);
  }, 2000); // Simulate a 2-second delay for fetching data
}

function displayData(data) {
  console.log("User data:", data);
}

fetchData(displayData);
```

- `fetchData` is a function that simulates an asynchronous operation using `setTimeout`.
- It takes a callback function as an argument and calls this callback with some data after 2 seconds.
- `displayData` is the callback function that logs the data to the console.
- When `fetchData(displayData)` is called, after 2 seconds, `displayData` is executed with the fetched data, resulting in `User data: { name: 'John', age: 30 }` being logged.

### Key Points

- **Asynchronous Operations**: Callbacks are essential for handling operations that don't complete immediately, like network requests or timers.
- **Higher-Order Functions**: Functions that take other functions as arguments or return functions are known as higher-order functions.
- **Error Handling**: Callbacks can also handle errors by following the common pattern of passing an error as the first argument to the callback.

#### Example with Error Handling

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const error = null;
    const data = { name: "John", age: 30 };
    callback(error, data);
  }, 2000);
}

function handleData(error, data) {
  if (error) {
    console.log("An error occurred:", error);
  } else {
    console.log("User data:", data);
  }
}

fetchData(handleData);
```

- Here, `fetchData` calls `callback` with an `error` (which is `null` in this case) and `data`.
- `handleData` checks if there's an error and logs the data accordingly.

### Summary

- **Callback**: A function passed to another function to be executed later.
- **Usage**: Commonly used for asynchronous operations.
- **Error Handling**: Can be used to handle errors in asynchronous operations.

Callbacks are a fundamental concept in JavaScript that enable powerful and flexible code, especially in dealing with asynchronous tasks.

---

13. why js is single threaded language

- JavaScript ek single-threaded language hai kyunki uska design esa hi banaya gaya hai. Matlab, JavaScript sirf ek hi thread me code ko execute karta hai. Iska reason yeh hai ki JavaScript web browsers me use hota hai jaha ek time pe ek hi kaam hona chahiye taaki user experience smooth rahe.

- JavaScript ki execution ek "call stack" aur "event loop" ke through hoti hai. Jab JavaScript code run hota hai, sabse pehle wo call stack me jaata hai. Call stack sequentially, ek ke baad ek, functions ko execute karta hai. Agar koi function call stack me aata hai, to pehle usse execute kiya jaata hai, aur phir stack se hata diya jaata hai.

- Event loop ensure karta hai ki browser responsive rahe. Jab bhi call stack empty hota hai, event loop check karta hai ki koi pending callback functions hain jo execute hone chahiye. Is tarah, asynchronous operations jaise setTimeout, AJAX requests, ya DOM events handle kiye jaate hain bina main thread ko block kiye.

- Single-threaded hone ka fayda yeh hai ki yeh race conditions aur deadlocks jaise problems ko avoid karta hai jo multi-threaded programming me aasani se ho sakti hain. Web development me, yeh simplicity aur efficiency provide karta hai.

- In short, JavaScript ka single-threaded nature usko simpler aur safer banata hai, especially jab hum web pages aur web applications develop karte hain.

---

14. `this`

JavaScript me `this` keyword bahut important aur thoda confusing concept ho sakta hai, kyunki iska value depend karta hai ki `this` kaise aur kahaan use ho raha hai. `this` typically us object ko refer karta hai jo current context me code execute kar raha hai.

### Different Contexts of `this`

1. **Global Context**
2. **Object Method**
3. **Constructor Function**
4. **Event Handlers**
5. **Arrow Functions**

### 1. Global Context

Global context me, `this` global object ko refer karta hai. Browser environment me, ye `window` object hota hai.

```javascript
console.log(this); // Browser me ye 'window' object ko print karega
```

### 2. Object Method

Agar `this` ko kisi object ke method me use kiya jaye, to ye us object ko refer karta hai.

```javascript
const person = {
  name: "John",
  greet: function () {
    console.log(this.name);
  },
};

person.greet(); // Output: John
```

Is example me, `this.name` `person` object ka `name` property refer karta hai.

### 3. Constructor Function

Constructor functions me, `this` newly created instance ko refer karta hai.

```javascript
function Person(name) {
  this.name = name;
}

const person1 = new Person("Alice");
console.log(person1.name); // Output: Alice
```

Yahan `this.name` nayi instance `person1` ka `name` property set kar raha hai.

### 4. Event Handlers

HTML event handlers me, `this` us element ko refer karta hai jisme event listener attached hota hai.

```html
<!DOCTYPE html>
<html>
  <body>
    <button id="myButton">Click me</button>
    <script>
      document
        .getElementById("myButton")
        .addEventListener("click", function () {
          console.log(this); // Output: <button id="myButton">Click me</button>
        });
    </script>
  </body>
</html>
```

### 5. Arrow Functions

Arrow functions me `this` lexically scoped hota hai, matlab jo `this` surrounding context (parent function ya global scope) me hota hai, wahi use hota hai.

```javascript
const person = {
  name: "John",
  greet: function () {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  },
};

person.greet(); // Output: John
```

Is example me, arrow function ka `this` us parent function (`greet` method) ka `this` refer karta hai.

### Manual Binding of `this`

Kabhi-kabhi aapko manually `this` ko bind karna padta hai, jo methods jaise `call`, `apply`, aur `bind` se hota hai.

#### `bind` Method

`bind` method naya function return karta hai jisme permanently `this` bind hota hai.

```javascript
const person = {
  name: "John",
  greet: function () {
    console.log(this.name);
  },
};

const greet = person.greet.bind(person);
greet(); // Output: John
```

#### `call` and `apply` Methods

`call` aur `apply` methods se aap `this` ko specify karke function ko immediately invoke kar sakte ho.

```javascript
const person1 = {
  name: "John",
};

const person2 = {
  name: "Alice",
};

function greet() {
  console.log(this.name);
}

greet.call(person1); // Output: John
greet.call(person2); // Output: Alice
```

### Summary

- **Global Context**: `this` global object (browser me `window`) ko refer karta hai.
- **Object Method**: `this` us object ko refer karta hai jisme method define kiya gaya hai.
- **Constructor Function**: `this` newly created instance ko refer karta hai.
- **Event Handlers**: `this` us HTML element ko refer karta hai jisme event listener attached hai.
- **Arrow Functions**: `this` lexically scoped hota hai, aur parent context ka `this` use karta hai.

Is tarah, JavaScript me `this` keyword ka behaviour context pe depend karta hai. Samajh ke aur sahi tarike se use karke aap apne code ko more predictable aur error-free bana sakte ho.
