

<table border="3">
        <tr>
            <th>S.no</th>
            <th>Topics</th>
        </tr>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
            <td>4</td>
            <td>5</td>
            <td>6</td>
        </tr>
        <tr>
            <td><a href="#Var">**Variables**</a></td>
            <td><a href="#Pri">**Primitives**</a></td>
            <td><a href="#Array">**Arrays**</a></td>
            <td><a href="#Obj">**Objects**</a></td>
            <td><a href="#Fun">**Function**</a></td>
            <td><a href="#Asy">**Asynchronous**</a></td>
        </tr>
    </table>
<h3 id="#Var">**Variables**</h3>

**1) Explain the difference between let, const, and var?**

Here’s an explanation of the differences between `let`, `const`, and `var` in JavaScript, summarized in a table with examples.
### **Difference Between `let`, `const`, and `var`**

| Feature                       | `var`                        | `let`                        | `const`                      |
|-------------------------------|------------------------------|------------------------------|------------------------------|
| **Scope**                     | Function or global scope     | Block scope                 | Block scope                 |
| **Re-declaration**            | Allowed within the same scope| Not allowed in the same scope| Not allowed in the same scope|
| **Initialization**            | Optional                    | Optional                    | Mandatory (requires a value at declaration) |
| **Reassignment**              | Allowed                     | Allowed                     | Not allowed                 |
| **Hoisting**                  | Hoisted and initialized as `undefined` | Hoisted but not initialized | Hoisted but not initialized |
| **Use Case**                  | Older code, avoid using in modern JavaScript | Variables that may change | Constants or immutable values |

---

### **Examples of Each**

#### **Using `var`**

```javascript
// Function scope
function testVar() {
  var x = 10;
  if (true) {
    var x = 20; // Same variable, redefined
    console.log(x); // 20
  }
  console.log(x); // 20 (not block-scoped)
}

testVar();

// Hoisting
console.log(a); // undefined
var a = 5;
```

---

#### **Using `let`**

```javascript
// Block scope
function testLet() {
  let x = 10;
  if (true) {
    let x = 20; // Different variable due to block scope
    console.log(x); // 20
  }
  console.log(x); // 10 (block-scoped)
}

testLet();

// Hoisting
// console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 5;
```

---

#### **Using `const`**

```javascript
// Block scope
function testConst() {
  const x = 10;
  if (true) {
    const x = 20; // Different variable due to block scope
    console.log(x); // 20
  }
  console.log(x); // 10 (block-scoped)
}

testConst();

// Reassignment
const c = 5;
// c = 10; // TypeError: Assignment to constant variable

// Hoisting
// console.log(d); // ReferenceError: Cannot access 'd' before initialization
const d = 5;
```

---

### Key Points to Remember

- **Use `let`** when a variable’s value needs to change.
- **Use `const`** for values that should not change (constants).
- **Avoid `var`** in modern JavaScript, as it can lead to bugs due to its function/global scope and hoisting behavior.


**2)Create Variables with Object and Array and Log Their Types?**
let user = {
    name: "Alice",
    age: 30
};
let colors = ["red", "green", "blue"];
 
console.log(typeof user); // "object"
console.log(typeof colors); // "object" (arrays are objects)


<h3 id="Pri">Pri</h3>










Both arrays and objects are identified as "object" type in JavaScript.


#**Primitives**:
1.How does hoisting work in JavaScript?
