# REACT-Cheat-Sheet
Functional React JavaScript Cheat Sheet. The JS (ES6+) features that Functional React relies on.

### 1. Array Methods (The Rendering Engines)

In functional React, you rarely use for loops. You transform arrays of data into arrays of JSX elements.
• .map() – Used constantly to loop through data and render lists of components.javascript
const users = ["Alice", "Bob", "Charlie"];
const listItems = users.map(user => `<li>${user}</li>`);
Use code with caution.
• .filter() – Used to remove items from lists (like deleting a todo item).javascript
const todos = [{id: 1, text: "Clean"}, {id: 2, text: "Cook"}];
const remaining = todos.filter(todo => todo.id !== 1); // Removes item 1
Use code with caution.

### 2. Destructuring (The Component Pipeline)

React passes data into components inside a single object called props. Destructuring lets you unpack that object instantly.
• Object Destructuring – Pulls properties right out of an object.javascript
const user = { name: "Bob", age: 30 };
const { name, age } = user; // Instantly creates variables 'name' and 'age'
Use code with caution.
• Array Destructuring – Pulls items out by position (this is exactly how useState hooks work).javascript
const coordinates = [45.5, -122.6];
const [lat, lng] = coordinates; 
Use code with caution.

### 3. Arrow Functions & Implicit Returns

Functional components are literally just functions. Short, clean syntax keeps your code readable.
• Explicit vs. Implicit – If an arrow function is one line, omit {} and return.javascript
// Explicit (Requires 'return' keyword)
const MyComponent = () => {
    return <h1>Hello</h1>;
};

// Implicit (Automatic return - ideal for simple JSX)
const MyComponentShort = () => <h1>Hello</h1>;
Use code with caution.

### 4. Template Literals & Logical Operators

React uses JavaScript logic inside JSX using curly braces {} to dynamically show, hide, or style things.
• Logical AND (&&) – The Conditional Render Shortcut. If the left side is true, it renders the right side.javascript
const isLoggedIn = true;
isLoggedIn && console.log("Show the Dashboard!"); 
Use code with caution.
• Ternary Operator (? :) – Used for if/else styling or text changes inside JSX.javascript
const isDarkMode = true;
const theme = isDarkMode ? "dark-theme" : "light-theme";
Use code with caution.
• Template Literals – Used to combine variable strings dynamically (perfect for dynamic class names).javascript
const className = `btn ${isActive ? "btn-active" : "btn-disabled"}`;
Use code with caution.

### 5. Spread Operator (...)

React state is immutable (you can't modify it directly). You must create a copy of arrays or objects when updating them.
• Copying Objects/Arrays – Spreads existing values into a new shell.javascript
const originalUser = { name: "Bob", role: "User" };
// Creates a brand new object, keeping old data but overriding the role
const updatedUser = { ...originalUser, role: "Admin" }; 

