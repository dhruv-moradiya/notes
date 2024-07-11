1. HTML

HTML (HyperText Markup Language) ek standard language hai jo web pages banane aur design karne ke liye use hoti hai. Yeh web pages ko structure aur unke content ko define karti hai, jisme tags aur attributes ka istemal hota hai. Yaha par HTML ke kuch key components aur features ka brief overview diya gaya hai:

### HTML ke Key Components:

1. **Elements**: HTML ke building blocks hain. Yeh usually ek start tag, content, aur ek end tag se bante hain.

   - Example: `<p>Yeh ek paragraph hai.</p>`

2. **Tags**: Keywords jo angle brackets me hoti hain. HTML tags usually pairs me aati hain: ek opening tag aur ek closing tag.

   - Opening tag: `<tagname>`
   - Closing tag: `</tagname>`
   - Kuch tags self-closing hoti hain, jaise `<img />`.

3. **Attributes**: Elements ke baare me additional information provide karti hain. Attributes hamesha opening tag me hoti hain.
   - Example: `<a href="https://www.example.com">Yeh ek link hai</a>`

### Ek HTML Document ka Basic Structure:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
    <h1>Yeh ek Heading hai</h1>
    <p>Yeh ek paragraph hai.</p>
    <a href="https://www.example.com">Yeh ek link hai</a>
  </body>
</html>
```

- **`<!DOCTYPE html>`**: Document type aur HTML version ko declare karta hai.
- **`<html>`**: Ek HTML page ka root element hota hai.
- **`<head>`**: HTML document ke baare me meta-information rakhta hai (jaise title, character set, styles, etc.).
- **`<title>`**: Document ka title specify karta hai, jo browser ke title bar ya tab me display hota hai.
- **`<body>`**: HTML document ka content rakhta hai jaise headings, paragraphs, links, images, aur other elements.

### Common HTML Tags:

- **Headings**: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`
- **Paragraphs**: `<p>`
- **Links**: `<a>`
- **Images**: `<img>`
- **Lists**:
  - Ordered: `<ol>` with `<li>`
  - Unordered: `<ul>` with `<li>`
- **Tables**: `<table>`, `<tr>`, `<td>`, `<th>`

### Attributes Examples:

- **href**: `<a>` tags me link ki URL specify karta hai.
- **src**: `<img>` tags me image ka path specify karta hai.
- **alt**: `<img>` tags me image ke liye alternative text provide karta hai.

### HTML Versions:

HTML kaafi evolve ho chuka hai, aur HTML5 latest standard hai. HTML5 ne kaafi naye elements aur attributes introduce kiye hain, jaise `<video>`, `<audio>`, aur `<canvas>`, jo multimedia content support aur modern web technologies ke sath better integration provide karte hain.

HTML web development ke liye fundamental hai aur often CSS (Cascading Style Sheets) aur JavaScript ke sath use hota hai taaki visually appealing aur interactive web pages banaye ja sake.

---

Flexbox aur Grid CSS ke do powerful layout systems hain jo web design mein use kiye jaate hain.

### Flexbox:

Flexbox (Flexible Box Layout) ek aisa layout module hai jo aapko elements ko ek direction mein (row ya column) align aur distribute karne mein madad karta hai. Iska main use responsive design ke liye hota hai, jahan elements ko easily center, space-between, ya evenly distribute kiya ja sakta hai.

#### Key Points:

- **Axis:** Flexbox do axis par kaam karta hai - main axis aur cross axis.
- **Main Axis:** Ye wo axis hai jisme elements arrange hote hain (horizontal ya vertical).
- **Flex Container:** Parent element ko flex container banaate hain aur uske andar ke elements flex items kehlate hain.
- **Properties:** `display: flex;`, `justify-content`, `align-items`, `flex-direction`, etc.

### Grid:

CSS Grid Layout ek 2D grid system hai jo rows aur columns dono mein elements ko arrange kar sakta hai. Ye complex layouts banane ke liye use hota hai jahan aapko rows aur columns dono mein control chahiye hota hai.

#### Key Points:

- **Grid Container:** Parent element ko grid container banaate hain aur uske andar ke elements grid items kehlate hain.
- **Grid Tracks:** Ye rows aur columns hain jo grid ko define karte hain.
- **Properties:** `display: grid;`, `grid-template-columns`, `grid-template-rows`, `gap`, `grid-area`, etc.

### Comparison:

- **Flexbox** zyada tar linear layout ke liye acha hai (ek direction mein).
- **Grid** complex aur 2D layouts ke liye behtar hai (rows aur columns dono mein).

In dono ka use karke aap responsive aur complex web designs easily bana sakte hain.

---

Inline-block aur block display properties CSS mein elements ko different tarikon se display karne ke liye use hoti hain.

### Block:

Block elements full width lete hain aur automatically next line par shift ho jaate hain. Yeh elements puri available width ko occupy karte hain.

#### Key Points:

- **Width & Height:** Block elements ko aap width aur height assign kar sakte hain.
- **Margin & Padding:** Block elements margins aur paddings ko vertically aur horizontally apply kar sakte hain.
- **Examples:** `<div>`, `<h1>`, `<p>`, `<section>`, etc.
- **Line Break:** Yeh elements apne baad ek line break create karte hain, matlab next element next line mein aayega.

### Inline-block:

Inline-block elements inline elements ki tarah behave karte hain, par yeh block elements ke kuch properties retain karte hain. Yeh elements apne content jitni width lete hain aur next elements ke saath inline rahte hain.

#### Key Points:

- **Width & Height:** Inline-block elements ko bhi width aur height assign kar sakte hain.
- **Margin & Padding:** Inline-block elements margins aur paddings ko vertically aur horizontally apply kar sakte hain.
- **Examples:** Custom elements using `display: inline-block;`.
- **No Line Break:** Yeh elements apne baad line break nahi create karte, matlab next element uske saath hi inline rahega.

### Comparison:

- **Block Element:** Puri line le leta hai aur next element next line mein shift ho jaata hai.
- **Inline-block Element:** Apne content ke width jitni width leta hai aur inline elements ki tarah behave karta hai, par usko width aur height assign kar sakte hain.

### Examples:

#### Block Element Example:

```html
<div style="display: block; background: lightblue;">Block Element 1</div>
<div style="display: block; background: lightcoral;">Block Element 2</div>
```

#### Inline-block Element Example:

```html
<div style="display: inline-block; background: lightblue; width: 100px;">
  Inline-block 1
</div>
<div style="display: inline-block; background: lightcoral; width: 100px;">
  Inline-block 2
</div>
```

Block elements full width lete hain aur next line mein shift ho jaate hain, jabki inline-block elements apne content jitna space leke saath-saath display hote hain.
