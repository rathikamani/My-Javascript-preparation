In CSS, the priority order (also known as specificity) determines which styles are applied when multiple rules target the same element. The priority follows this order:

### **1. Inline Styles** (Highest Priority)
- Styles written directly inside an element using the `style` attribute.
- Example:  
  ```html
  <p style="color: red;">This text is red.</p>
  ```

### **2. ID Selectors**
- Styles applied using an `id` selector (`#id`).
- Example:  
  ```css
  #example {
    color: blue;
  }
  ```

### **3. Class, Attribute, and Pseudo-class Selectors**
- Styles applied using `.class`, `[attribute]`, and `:pseudo-class`.
- Example:  
  ```css
  .example {
    color: green;
  }
  ```

### **4. Element (Tag) Selectors**
- Styles applied to HTML elements directly.
- Example:  
  ```css
  p {
    color: orange;
  }
  ```

### **5. Universal Selector and Inherited Styles (Lowest Priority)**
- The `*` selector or inherited properties from parent elements.
- Example:  
  ```css
  * {
    color: black;
  }
  ```

### **!important (Overrides All Other Rules)**
- Any rule with `!important` takes precedence over all other rules, regardless of specificity.
- Example:  
  ```css
  p {
    color: purple !important;
  }
  ```

### **Final Priority Order (From Highest to Lowest)**
1. **Inline styles (`style=""`)**
2. **ID selectors (`#id`)**
3. **Class, attribute, and pseudo-class selectors (`.class`, `[attr]`, `:hover`, etc.)**
4. **Element (tag) selectors (`div`, `p`, `h1`, etc.)**
5. **Universal selector (`*`) and inherited styles**
6. **Browser default styles**



CSS selectors are used to target HTML elements for styling. Below are the most common CSS selectors with examples:

---

### **1. Universal Selector (`*`)**
- Applies to all elements.
```css
* {
  margin: 0;
  padding: 0;
}
```

---

### **2. Element (Type) Selector**
- Targets all instances of a specific HTML tag.
```css
p {
  color: blue;
}
```
```html
<p>This paragraph will be blue.</p>
```

---

### **3. Class Selector (`.class`)**
- Targets elements with a specific class.
```css
.red-text {
  color: red;
}
```
```html
<p class="red-text">This text is red.</p>
```

---

### **4. ID Selector (`#id`)**
- Targets a specific element by its ID.
```css
#main-title {
  font-size: 24px;
}
```
```html
<h1 id="main-title">This is a heading</h1>
```

---

### **5. Group Selector (`,`)**
- Applies styles to multiple elements at once.
```css
h1, h2, p {
  font-family: Arial, sans-serif;
}
```

---

### **6. Descendant Selector (`element1 element2`)**
- Targets elements inside a specific parent.
```css
div p {
  color: green;
}
```
```html
<div>
  <p>This paragraph inside div will be green.</p>
</div>
```

---

### **7. Child Selector (`>` )**
- Targets direct children of a parent element.
```css
div > p {
  font-weight: bold;
}
```
```html
<div>
  <p>This paragraph will be bold.</p>
</div>
```

---

### **8. Adjacent Sibling Selector (`+`)**
- Selects the next **immediate** sibling element.
```css
h1 + p {
  color: purple;
}
```
```html
<h1>Heading</h1>
<p>This paragraph will be purple.</p>
```

---

### **9. General Sibling Selector (`~`)**
- Selects **all** siblings after a specific element.
```css
h1 ~ p {
  color: pink;
}
```
```html
<h1>Title</h1>
<p>First paragraph.</p>
<p>Second paragraph.</p>
```

---

### **10. Attribute Selector (`[attr]`)**
- Selects elements with a specific attribute.
```css
input[type="text"] {
  border: 2px solid blue;
}
```
```html
<input type="text" placeholder="Text input">
<input type="password" placeholder="Password">
```
*(Only the text input will have a blue border.)*

---

### **11. Pseudo-classes (`:hover`, `:focus`, etc.)**
- Targets elements in a specific state.
```css
button:hover {
  background-color: yellow;
}
```
```html
<button>Hover me</button>
```

---

### **12. Pseudo-elements (`::before`, `::after`)** 
- Inserts content before or after an element.
```css
p::before {
  content: "👉 ";
}
```
```html
<p>Important note</p>
```
*(The paragraph will display with a pointing emoji at the start.)*

---

