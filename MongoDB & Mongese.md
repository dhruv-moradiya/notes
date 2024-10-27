- [Comparison Operators](#comparison-operators)
- [Logical Operators](#logical-operators)
- [Arithmetic Operators](#arithmetic-operators)

1. [How ObjectId work in Schema](#how-objectid-work-in-schema)
2. [What is Aggregate?](#what-is-aggregate)
3. [$match](#match)
4. [$group](#group)
5. [$lookup](#lookup)
6. [$project](#project)

---

MongoDB aggregation framework mein kai operators hote hain jo different types of operations perform karte hain. Yeh operators aapko data ko filter, transform, group, aur manipulate karne mein madad karte hain. Neeche kuch common operators aur unke uses diye gaye hain:

### Comparison Operators

- **`$eq`**: Equal to (Barabar)
- **`$ne`**: Not equal to (Barabar nahi)
- **`$gt`**: Greater than (Se zyada)
- **`$gte`**: Greater than or equal to (Se zyada ya barabar)
- **`$lt`**: Less than (Se kam)
- **`$lte`**: Less than or equal to (Se kam ya barabar)
- **`$in`**: Matches any of the values specified in an array (Diye gaye array mein se kisi bhi value se match kare)
- **`$nin`**: Matches none of the values specified in an array (Diye gaye array mein se kisi bhi value se match nahi kare)

Comparison operators in Mongoose allow you to filter documents in your MongoDB collections based on specific criteria. These operators are used in queries to compare field values against specified values. Here's a brief explanation in Hinglish along with examples:

### Mongoose Model Setup

Maan lo ki humare paas ek `User` model hai:

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  city: String,
});

const User = mongoose.model("User", userSchema);
```

### Examples of Comparison Operators

1. **$eq (equal to)**

   Matlab yeh operator tab use hota hai jab humein kisi specific value ke barabar records chahiyein.

   ```javascript
   // Users jo 25 saal ke hain
   User.find({ age: { $eq: 25 } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

2. **$ne (not equal to)**

   Matlab yeh operator tab use hota hai jab humein specific value ke alawa sab chahiyein.

   ```javascript
   // Users jo 25 saal ke nahi hain
   User.find({ age: { $ne: 25 } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

3. **$gt (greater than)**

   Matlab yeh operator tab use hota hai jab humein kisi specific value se zyada wale records chahiyein.

   ```javascript
   // Users jo 25 saal se bade hain
   User.find({ age: { $gt: 25 } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

4. **$gte (greater than or equal to)**

   Matlab yeh operator tab use hota hai jab humein kisi specific value se zyada ya barabar wale records chahiyein.

   ```javascript
   // Users jo 25 saal ya usse bade hain
   User.find({ age: { $gte: 25 } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

5. **$lt (less than)**

   Matlab yeh operator tab use hota hai jab humein kisi specific value se kam wale records chahiyein.

   ```javascript
   // Users jo 25 saal se kam ke hain
   User.find({ age: { $lt: 25 } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

6. **$lte (less than or equal to)**

   Matlab yeh operator tab use hota hai jab humein kisi specific value se kam ya barabar wale records chahiyein.

   ```javascript
   // Users jo 25 saal ya usse kam ke hain
   User.find({ age: { $lte: 25 } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

7. **$in (in array)**

   Matlab yeh operator tab use hota hai jab humein specific values ke andar wale records chahiyein.

   ```javascript
   // Users jo 20, 25 ya 30 saal ke hain
   User.find({ age: { $in: [20, 25, 30] } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

8. **$nin (not in array)**

   Matlab yeh operator tab use hota hai jab humein specific values ke bahar wale records chahiyein.

   ```javascript
   // Users jo 20, 25 ya 30 saal ke nahi hain
   User.find({ age: { $nin: [20, 25, 30] } })
     .then((users) => console.log(users))
     .catch((err) => console.error(err));
   ```

### Full Example in Mongoose

Agar aap poora code run karna chahte hain, toh pehle Mongoose aur MongoDB connect karna zaroori hai:

```javascript
const mongoose = require("mongoose");

mongoose
  .connect("mongodb://localhost:27017/mydatabase", {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  })
  .then(() => {
    console.log("MongoDB connected");

    // Yahan pe apne queries run kar sakte hain

    // Example: Users jo 25 saal ke hain
    return User.find({ age: { $eq: 25 } });
  })
  .then((users) => console.log(users))
  .catch((err) => console.error(err))
  .finally(() => mongoose.disconnect());
```

Is tarah se aap comparison operators ka use karke MongoDB me filtered queries run kar sakte hain Mongoose ke saath.

### Logical Operators

- **`$and`**: Joins query clauses with a logical AND returns all documents that match the conditions of both clauses (Logical AND operation)
- **`$or`**: Joins query clauses with a logical OR returns all documents that match the conditions of either clause (Logical OR operation)
- **`$not`**: Inverts the effect of a query expression and returns documents that do not match the query expression (Logical NOT operation)
- **`$nor`**: Joins query clauses with a logical NOR returns all documents that fail to match both clauses (Logical NOR operation)

### Arithmetic Operators

- **`$add`**: Adds numbers together (Jodne ke liye)
- **`$subtract`**: Subtracts second value from the first (Ghatane ke liye)
- **`$multiply`**: Multiplies numbers together (Gune ke liye)
- **`$divide`**: Divides the first number by the second (Bhag karne ke liye)
- **`$mod`**: Divides the first number by the second and returns the remainder (Modulus operation)

### Array Operators (Array ke liye)

- **`$arrayElemAt`**: Returns the element at the specified array index (Specified index pe element ko return karta hai)
- **`$concatArrays`**: Concatenates arrays to return a new array (Arrays ko concatenate karta hai)
- **`$filter`**: Selects a subset of the array to return based on the specified condition (Condition ke basis pe array ka subset select karta hai)
- **`$in`**: Returns whether a specified value is in an array (Check karta hai ki value array mein hai ya nahi)
- **`$size`**: Returns the number of elements in the array (Array mein elements ki count return karta hai)

### String Operators (Strings ke liye)

- **`$concat`**: Concatenates multiple strings into a single string (Multiple strings ko ek string mein concatenate karta hai)
- **`$substr`**: Returns a substring of a string, starting at a specified index position (String ka substring return karta hai)
- **`$toLower`**: Converts a string to lowercase (String ko lowercase mein convert karta hai)
- **`$toUpper`**: Converts a string to uppercase (String ko uppercase mein convert karta hai)
- **`$trim`**: Removes whitespace or the specified characters from the beginning and end of a string (String ke beginning aur end se whitespace ya specified characters ko remove karta hai)

### Date Operators (Tarikh ke liye)

- **`$dateToString`**: Converts a date object to a string (Date object ko string mein convert karta hai)
- **`$dayOfMonth`**: Returns the day of the month for a date as a number (Date ke liye month ka day return karta hai)
- **`$dayOfWeek`**: Returns the day of the week for a date as a number (Date ke liye week ka day return karta hai)
- **`$dayOfYear`**: Returns the day of the year for a date as a number (Date ke liye year ka day return karta hai)
- **`$month`**: Returns the month for a date as a number (Date ke liye month return karta hai)
- **`$year`**: Returns the year for a date as a number (Date ke liye year return karta hai)
- **`$hour`**: Returns the hour for a date as a number (Date ke liye hour return karta hai)
- **`$minute`**: Returns the minute for a date as a number (Date ke liye minute return karta hai)
- **`$second`**: Returns the second for a date as a number (Date ke liye second return karta hai)
- **`$millisecond`**: Returns the millisecond for a date as a number (Date ke liye millisecond return karta hai)

### Aggregation Operators (Sangrahak)

- **`$sum`**: Returns the sum of all numerical values that result from applying a specified expression to each document in a group of documents that share the same group by key (Numerical values ka sum return karta hai)
- **`$avg`**: Returns the average value of the numerical values that result from applying a specified expression to each document in a group of documents that share the same group by key (Numerical values ka average return karta hai)
- **`$min`**: Returns the minimum value (Minimum value return karta hai)
- **`$max`**: Returns the maximum value (Maximum value return karta hai)
- **`$first`**: Returns the first value (Pehla value return karta hai)
- **`$last`**: Returns the last value (Aakhri value return karta hai)
- **`$push`**: Returns an array of values (Values ka array return karta hai)
- **`$addToSet`**: Returns an array with unique values (Unique values ka array return karta hai)

### Conditional Operators (Shartein)

- **`$cond`**: Evaluates a condition and returns one of two expressions (Condition evaluate karke do expressions mein se ek return karta hai)
- **`$ifNull`**: Returns a value if a specified expression evaluates to null (Null hone pe ek specified value return karta hai)

### Other Useful Operators

- **`$type`**: Returns the BSON type of the field (Field ka BSON type return karta hai)
- **`$regex`**: Provides regular expression capabilities for pattern matching strings (Pattern matching ke liye regular expression capabilities provide karta hai)
- **`$geoNear`**: Returns documents based on proximity to a geospatial point (Geospatial point ke proximity ke basis pe documents return karta hai)

Yeh kuch common operators hain jo MongoDB aggregation framework mein available hain. Inhe use karke aap complex queries aur data manipulations perform kar sakte hain.

---

MongoDB aggregation pipeline mein kaafi saare stages available hain jo aapko complex data manipulations aur transformations perform karne ki suvidha dete hain. `$match`, `$group`, `$lookup`, aur `$project` ke alawa, neeche kuch aur commonly used aggregation stages diye gaye hain:

1. **`$addFields`**: Naye fields add karne ke liye ya existing fields ko modify karne ke liye.
2. **`$bucket`**: Values ko range-based buckets mein divide karne ke liye.
3. **`$bucketAuto`**: Values ko automatically calculated buckets mein divide karne ke liye.
4. **`$count`**: Documents count karne ke liye aur result mein total count return karne ke liye.
5. **`$facet`**: Multiple pipelines ko ek hi stage mein run karne ke liye aur combined result return karne ke liye.
6. **`$geoNear`**: Geospatial documents ko proximity ke basis pe sort aur return karne ke liye.
7. **`$limit`**: Documents ki count limit karne ke liye jo pipeline se pass hoti hain.
8. **`$sort`**: Documents ko specified fields ke basis pe sort karne ke liye.
9. **`$skip`**: Specified count ke documents ko skip karne ke liye.
10. **`$unwind`**: Array fields ko deconstruct karke har element ko alag document banane ke liye.
11. **`$replaceRoot`**: Document ke root ko replace karne ke liye specified sub-document ke saath.
12. **`$sample`**: Random documents ko sample karne ke liye.
13. **`$merge`**: Aggregation results ko existing collection mein merge ya output karne ke liye.
14. **`$out`**: Aggregation results ko ek specified collection mein write karne ke liye.
15. **`$sortByCount`**: Documents ko group aur sort karne ke liye count ke basis pe.
16. **`$redact`**: Documents ko filter karne ke liye specified access level ke basis pe.

**In aggregation stages ka use karke aap complex queries aur data transformations easily perform kar sakte hain.**

**Example of using multiple stages in a pipeline:**

```javascript
db.orders
  .aggregate([
    {
      $match: { status: "A" }, // Filter documents with status "A"
    },
    {
      $group: {
        _id: "$cust_id",
        totalAmount: { $sum: "$amount" },
      }, // Group by customer ID and calculate total amount
    },
    {
      $sort: { totalAmount: -1 }, // Sort by total amount in descending order
    },
    {
      $limit: 5, // Limit to top 5 results
    },
  ])
  .then((result) => {
    console.log(result); // Process the result
  })
  .catch((err) => {
    console.error(err); // Handle the error
  });
```

Is example mein humne multiple stages ko combine kiya hai jismein `$match`, `$group`, `$sort`, aur `$limit` include hain. Aggregation pipeline ka power yahi hai ki aap multiple stages ko chain kar sakte hain aur complex queries aur transformations easily perform kar sakte hain.

---

👉 `$multiply`

`$multiply` MongoDB aggregation framework ka ek operator hai jo numbers ko multiply karne ke liye use hota hai. Yeh operator aapko aggregation pipeline mein fields ko multiply karne ki suvidha deta hai.

**Kaise kaam karta hai:**

- `$multiply` ek array accept karta hai jismein do ya zyada numbers ya fields hote hain jinhe multiply kiya jata hai.
- Har element array mein ya to ek number ho sakta hai ya ek field ka reference ho sakta hai.

**Example:**

Maan lo humare paas ek `orders` collection hai jismein har order ka `quantity` aur `pricePerUnit` field hai. Hume har order ka `totalPrice` calculate karna hai by multiplying `quantity` aur `pricePerUnit`. Yeh aise kiya ja sakta hai:

```javascript
Order.aggregate([
  {
    $project: {
      productId: 1, // productId field ko include karo
      quantity: 1, // quantity field ko include karo
      pricePerUnit: 1, // pricePerUnit field ko include karo
      totalPrice: { $multiply: ["$quantity", "$pricePerUnit"] }, // quantity aur pricePerUnit ko multiply karke totalPrice create karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `productId: 1`, `quantity: 1`, aur `pricePerUnit: 1`: Yeh fields ko include karne ke liye specify kiya gaya hai.
- `totalPrice: { $multiply: ["$quantity", "$pricePerUnit"] }`: Yeh `totalPrice` field ko define karta hai jo `quantity` aur `pricePerUnit` ko multiply karke calculate kiya gaya hai.

**Aur ek example:**

Agar aapko har product ka `totalCost` calculate karna hai jismein `quantity`, `pricePerUnit`, aur `tax` ko multiply karna hai:

```javascript
Product.aggregate([
  {
    $project: {
      productName: 1, // productName field ko include karo
      quantity: 1, // quantity field ko include karo
      pricePerUnit: 1, // pricePerUnit field ko include karo
      tax: 1, // tax field ko include karo
      totalCost: { $multiply: ["$quantity", "$pricePerUnit", "$tax"] }, // quantity, pricePerUnit aur tax ko multiply karke totalCost create karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `productName: 1`, `quantity: 1`, `pricePerUnit: 1`, aur `tax: 1`: Yeh fields ko include karne ke liye specify kiya gaya hai.
- `totalCost: { $multiply: ["$quantity", "$pricePerUnit", "$tax"] }`: Yeh `totalCost` field ko define karta hai jo `quantity`, `pricePerUnit`, aur `tax` ko multiply karke calculate kiya gaya hai.

Is tarah se `$multiply` operator ka use karke aap aggregation pipeline mein fields ko multiply kar sakte hain aur complex calculations perform kar sakte hain.

---

## How ObjectId work in Schema

```javascript
subscriber: {
  type: Schema.Types.ObjectId,
  ref: "User"
},
channel: {
  type: Schema.Types.ObjectId,
  ref: "User"
}
```

Iska matlab yeh hai ki `Subscription` schema mein `subscriber` aur `channel` dono fields hain jo `User` model ke `ObjectId` ko refer karti hain.

**Kaise kaam karta hai:**

- `subscriber` field: Yeh user ka `ObjectId` store karega jo kisi channel ko subscribe kar raha hai.
- `channel` field: Yeh user ka `ObjectId` store karega jisko subscribe kiya ja raha hai.

**Kis tarah ka data aayega:**

- `subscriber`: Yeh ek `User` ka unique `ObjectId` hoga jo subscribe karta hai.
- `channel`: Yeh bhi ek `User` ka unique `ObjectId` hoga jisko subscribe kiya ja raha hai.

Example ke liye, agar ek user "A" ne user "B" ko subscribe kiya, toh `Subscription` document kuch aisa dikhega:

```json
{
  "subscriber": "60d0fe4f5311236168a109ca",
  "channel": "60d0fe4f5311236168a109cb"
}
```

Yahan pe `"60d0fe4f5311236168a109ca"` user "A" ka `ObjectId` hai aur `"60d0fe4f5311236168a109cb"` user "B" ka `ObjectId` hai.

---

## what is aggregate ?

Mongoose mein, `aggregate` ek powerful feature hai jo aapko complex data aggregation operations perform karne ki suvidha deti hai MongoDB ke aggregation framework ka use karke. Yeh feature kaam aata hai jab aapko multiple documents se data ko filter, group, sort, aur transform karna hota hai.

**Kaise kaam karta hai:**

`aggregate` method ek array of stages ko accept karta hai, jahan har stage ek specific operation perform karti hai. Yeh stages ek pipeline ke tarah kaam karti hain, jahan ek stage ka output next stage ke input ke roop mein use hota hai.

**Common stages:**

1. `$match`: Documents ko filter karta hai jo specific criteria match karte hain.
2. `$group`: Documents ko group karta hai aur aggregation operations perform karta hai, jaise ki sum, average, etc.
3. `$project`: Documents ke specific fields ko select ya modify karta hai.
4. `$sort`: Documents ko sort karta hai kisi specific field ke basis par.
5. `$limit`: Documents ki output count ko limit karta hai.
6. `$lookup`: Ek collection se doosri collection mein join karta hai.

**Example:**

Agar humare paas ek `orders` collection hai aur hume total sales by product calculate karna hai, toh hum kuch aisa use kar sakte hain:

```javascript
Order.aggregate([
  { $match: { status: "completed" } }, // Sirf completed orders ko match karo
  { $group: { _id: "$productId", totalSales: { $sum: "$amount" } } }, // Product ke basis pe group karo aur total sales calculate karo
  { $sort: { totalSales: -1 } }, // Total sales ke basis pe descending order mein sort karo
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

1. `$match` stage sirf completed orders ko filter karta hai.
2. `$group` stage orders ko `productId` ke basis par group karta hai aur total sales calculate karta hai.
3. `$sort` stage total sales ke basis par result ko descending order mein sort karta hai.

Aise aap complex queries aur data transformations easily perform kar sakte hain `aggregate` method ka use karke.

---

## $match

Mongoose mein, `$match` ek aggregation pipeline stage hai jo documents ko filter karne ke liye use hota hai. Yeh bilkul waise hi kaam karta hai jaise ki SQL mein `WHERE` clause hota hai. `$match` stage ko pipeline mein sabse pehle use kiya jata hai taaki sirf wahi documents aggregation pipeline ke through pass ho jo specific criteria ko match karte hain.

**Kaise kaam karta hai:**

- `$match` ek object ko accept karta hai jo filtering criteria define karta hai.
- Yeh criteria key-value pairs ke form mein hota hai jahan key document field ka naam hota hai aur value matching condition hoti hai.

**Example:**

Maan lo humare paas ek `users` collection hai aur hume sirf un users ko filter karna hai jinka age 18 se zyada hai. Yeh aise kiya ja sakta hai:

```javascript
User.aggregate([
  { $match: { age: { $gt: 18 } } }, // Age greater than 18 wale users ko match karo
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `{ $match: { age: { $gt: 18 } } }`: Yeh stage `users` collection mein se sirf un documents ko filter karega jahan `age` field 18 se zyada ho (`$gt` ka matlab "greater than").

**Aur kuch common operators:**

- `$eq`: Equal to (barabar)
- `$ne`: Not equal to (barabar nahi)
- `$lt`: Less than (se kam)
- `$lte`: Less than or equal to (se kam ya barabar)
- `$gt`: Greater than (se zyada)
- `$gte`: Greater than or equal to (se zyada ya barabar)
- `$in`: Matches any of the values specified in an array (diye gaye array mein se kisi bhi value se match kare)
- `$nin`: Matches none of the values specified in an array (diye gaye array mein se kisi bhi value se match nahi kare)

**Aur ek example:**

Maan lo hume un users ko filter karna hai jo Mumbai mein rehte hain aur jinka age 25 se zyada hai:

```javascript
User.aggregate([
  { $match: { city: "Mumbai", age: { $gt: 25 } } }, // Mumbai mein rehne wale aur jinki age 25 se zyada hai unhe match karo
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `{ city: "Mumbai", age: { $gt: 25 } }`: Yeh stage un documents ko match karega jahan `city` "Mumbai" hai aur `age` 25 se zyada hai.

Is tarah se `$match` stage ka use karke aap aggregation pipeline mein specific documents ko filter kar sakte hain jo aapke criteria ko match karte hain.

---

## $group

Mongoose mein, `$group` ek aggregation pipeline stage hai jo documents ko group karne ke liye use hota hai aur har group par aggregation operations perform karne ki suvidha deta hai. Yeh bilkul waise hi kaam karta hai jaise ki SQL mein `GROUP BY` clause hota hai.

**Kaise kaam karta hai:**

- `$group` stage ek object ko accept karta hai jo group criteria aur aggregation expressions define karta hai.
- Is object mein `_id` field mandatory hoti hai jo grouping key define karti hai. Baaki fields aggregation operations define karti hain jo har group ke liye calculate kiya jata hai.

**Example:**

Maan lo humare paas ek `orders` collection hai aur hume total sales by product calculate karna hai. Yeh aise kiya ja sakta hai:

```javascript
Order.aggregate([
  {
    $group: {
      _id: "$productId", // Product ke basis pe group karo
      totalSales: { $sum: "$amount" }, // Har group (product) ke liye total sales calculate karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `_id: "$productId"`: Yeh define karta hai ki documents ko `productId` field ke basis pe group kiya jayega.
- `totalSales: { $sum: "$amount" }`: Yeh define karta hai ki har group ke liye `amount` field ka sum calculate kiya jayega aur `totalSales` field mein store kiya jayega.

**Common aggregation operators:**

- `$sum`: Values ka sum calculate karta hai.
- `$avg`: Values ka average calculate karta hai.
- `$min`: Minimum value ko find karta hai.
- `$max`: Maximum value ko find karta hai.
- `$first`: Har group mein pehla document return karta hai.
- `$last`: Har group mein akhri document return karta hai.
- `$push`: Har group mein values ko array ke roop mein store karta hai.
- `$addToSet`: Har group mein unique values ko array ke roop mein store karta hai.

**Aur ek example:**

Maan lo hume `users` collection mein har city ke total users aur average age calculate karna hai:

```javascript
User.aggregate([
  {
    $group: {
      _id: "$city", // City ke basis pe group karo
      totalUsers: { $sum: 1 }, // Har city ke liye total users count karo
      averageAge: { $avg: "$age" }, // Har city ke liye average age calculate karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `_id: "$city"`: Yeh define karta hai ki documents ko `city` field ke basis pe group kiya jayega.
- `totalUsers: { $sum: 1 }`: Yeh define karta hai ki har city ke liye total users count kiya jayega.
- `averageAge: { $avg: "$age" }`: Yeh define karta hai ki har city ke liye `age` field ka average calculate kiya jayega.

Is tarah se `$group` stage ka use karke aap documents ko group kar sakte hain aur har group ke liye specific aggregation operations perform kar sakte hain.

---

## $lookup

Mongoose mein, `$lookup` ek aggregation pipeline stage hai jo do alag-alag collections ke documents ko join karne ke liye use hota hai. Yeh bilkul waise hi kaam karta hai jaise ki SQL mein `JOIN` clause hota hai.

**Kaise kaam karta hai:**

- `$lookup` stage ek object ko accept karta hai jo join operation ko define karta hai. Is object mein kuch required fields hote hain:
  - `from`: Us collection ka naam jisse join karna hai.
  - `localField`: Source collection ka wo field jo join key ke roop mein use hota hai.
  - `foreignField`: Target collection ka wo field jo join key ke roop mein use hota hai.
  - `as`: Join ke result ko store karne ke liye new field ka naam.

**Example:**

Maan lo humare paas do collections hain: `orders` aur `customers`. Hum chahte hain ki har order ke saath corresponding customer ka data bhi aaye. Yeh aise kiya ja sakta hai:

```javascript
Order.aggregate([
  {
    $lookup: {
      from: "customers", // Join customers collection se
      localField: "customerId", // orders collection ka field jo join key hai
      foreignField: "_id", // customers collection ka field jo join key hai
      as: "customerDetails", // Join result ko store karne ke liye new field ka naam
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `from: "customers"`: Yeh specify karta hai ki join `customers` collection se hoga.
- `localField: "customerId"`: Yeh `orders` collection ka wo field specify karta hai jo join key ke roop mein use hota hai.
- `foreignField: "_id"`: Yeh `customers` collection ka wo field specify karta hai jo join key ke roop mein use hota hai.
- `as: "customerDetails"`: Yeh specify karta hai ki join result ko `customerDetails` field mein store kiya jayega.

**Aur ek example:**

Maan lo humare paas do collections hain: `users` aur `posts`. Hum chahte hain ki har user ke saath unke sabhi posts bhi aaye. Yeh aise kiya ja sakta hai:

```javascript
User.aggregate([
  {
    $lookup: {
      from: "posts", // Join posts collection se
      localField: "_id", // users collection ka field jo join key hai
      foreignField: "userId", // posts collection ka field jo join key hai
      as: "userPosts", // Join result ko store karne ke liye new field ka naam
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `from: "posts"`: Yeh specify karta hai ki join `posts` collection se hoga.
- `localField: "_id"`: Yeh `users` collection ka wo field specify karta hai jo join key ke roop mein use hota hai.
- `foreignField: "userId"`: Yeh `posts` collection ka wo field specify karta hai jo join key ke roop mein use hota hai.
- `as: "userPosts"`: Yeh specify karta hai ki join result ko `userPosts` field mein store kiya jayega.

Is tarah se `$lookup` stage ka use karke aap do alag-alag collections ke documents ko join kar sakte hain aur ek combined result pa sakte hain.

---

## $project

Mongoose mein, `$project` ek aggregation stage hai jo documents ke fields ko select ya modify karne ke liye use hota hai. Yeh stage aapko specific fields ko include ya exclude karne ki suvidha deti hai, aur naye fields ko calculate ya create karne ka option bhi provide karti hai.

**Kaise kaam karta hai:**

- `$project` stage ek object ko accept karta hai jismein key-value pairs hote hain. Har key document field ka naam hota hai aur value decide karti hai ki us field ko include/exclude karna hai ya nahi.
- `1` ka matlab include karna, `0` ka matlab exclude karna hota hai.
- Naye fields ko expressions ya existing fields ko combine karke bhi create kiya ja sakta hai.

**Example:**

Maan lo humare paas ek `users` collection hai aur hume sirf `username` aur `email` fields ko include karna hai:

```javascript
User.aggregate([
  {
    $project: {
      username: 1, // username field ko include karo
      email: 1, // email field ko include karo
      _id: 0, // _id field ko exclude karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `username: 1`: Yeh define karta hai ki `username` field ko include karna hai.
- `email: 1`: Yeh define karta hai ki `email` field ko include karna hai.
- `_id: 0`: Yeh define karta hai ki `_id` field ko exclude karna hai (by default `_id` include hota hai agar explicitly exclude nahi kiya gaya ho).

**Naye fields create karna:**

Aap existing fields ko use karke naye fields bhi create kar sakte hain. Maan lo hume `fullName` field ko `firstName` aur `lastName` fields ko combine karke create karna hai:

```javascript
User.aggregate([
  {
    $project: {
      firstName: 1, // firstName field ko include karo
      lastName: 1, // lastName field ko include karo
      fullName: { $concat: ["$firstName", " ", "$lastName"] }, // firstName aur lastName ko combine karke fullName create karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `firstName: 1` aur `lastName: 1`: Yeh dono fields ko include karta hai.
- `fullName: { $concat: ["$firstName", " ", "$lastName"] }`: Yeh define karta hai ki `fullName` field ko `firstName` aur `lastName` ko concatenate karke create karna hai.

**Aur ek example:**

Maan lo hume `orders` collection mein se `productId`, `quantity`, aur `totalPrice` calculate karke include karna hai jahan `totalPrice` ko `quantity` aur `pricePerUnit` ko multiply karke calculate karna hai:

```javascript
Order.aggregate([
  {
    $project: {
      productId: 1, // productId field ko include karo
      quantity: 1, // quantity field ko include karo
      totalPrice: { $multiply: ["$quantity", "$pricePerUnit"] }, // quantity aur pricePerUnit ko multiply karke totalPrice create karo
    },
  },
])
  .then((result) => {
    console.log(result); // Result ko process karo
  })
  .catch((err) => {
    console.error(err); // Error ko handle karo
  });
```

Is example mein:

- `productId: 1` aur `quantity: 1`: Yeh dono fields ko include karta hai.
- `totalPrice: { $multiply: ["$quantity", "$pricePerUnit"] }`: Yeh define karta hai ki `totalPrice` field ko `quantity` aur `pricePerUnit` ko multiply karke create karna hai.

Is tarah se `$project` stage ka use karke aap documents ke specific fields ko select, exclude, ya modify kar sakte hain aur naye fields ko create kar sakte hain.
