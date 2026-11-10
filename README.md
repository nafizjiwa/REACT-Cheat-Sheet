# REACT-Cheat-Sheet

#### Things to Review:
Static Pages
1. JSX
2. Custom components

Data Driven Pages
3. Component reuseability
4. Props help create reuseability
5. Creating components from an array of Data using array methods
Interactive Pages
6. Event listeners to interact in React and update app or API's
7. State in React to maintain data between re-renders
8. Declarative React API to only change Data that changed
9. Conditional Rendering using state
10. React Forms to take data from UI and use it
11. State management and where it is held
Side Effects
12. Controlled components
13. React Functional programming and side effects
14. Fetching Data with React when API loads
15. Side Effects and applying them in REACT
React Router
16. Next.js for front end or back end
17. Node.js in back end for REST API's 


## Functional React JavaScript. 
## Features that Functional React relies on.

### 1. Array Methods (The Rendering Engines)

Functional React rarely uses for loops. Arrays of data transformed into arrays of JSX elements.
• .map() – For looping through data and render lists of components.
JS
const users = ["Alice", "Bob", "Charlie"];
const listItems = users.map(user => `<li>${user}</li>`);

• .filter() – Removes items from lists (like deleting a todo item).
JS
const todos = [{id: 1, text: "Clean"}, {id: 2, text: "Cook"}];
const remaining = todos.filter(todo => todo.id !== 1); // Removes item 1

### 2. Destructuring (The Component Pipeline)

React passes data into components through a single object called props. Destructuring unpacks an object.
• Object Destructuring – Pulls properties out of an object.
JS
const user = { name: "Bob", age: 30 };
const { name, age } = user; // Instantly creates variables 'name' and 'age'

• Array Destructuring – Pulls items out by position (this is exactly how useState hooks work).
JS
const coordinates = [45.5, -122.6];
const [lat, lng] = coordinates; 

### 3. Arrow Functions & Implicit Returns

Functional components are functions.
• Explicit vs. Implicit – Single line arrow functions omit {} and return.
JS
// Explicit (Requires 'return' keyword)
const MyComponent = () => {
    return <h1>Hello</h1>;
};

// Implicit (Automatic return - simple JSX)
const MyComponentShort = () => <h1>Hello</h1>;

### 4. Template Literals & Logical Operators

React uses JavaScript logic inside JSX using curly braces {} to dynamically show, hide, or style things.
• Logical AND (&&) – (Conditional) If the left side is true, render right side.
JS
const isLoggedIn = true;
isLoggedIn && console.log("Show the Dashboard!"); 

• Ternary Operator (? :) – Used for if/else inside JSX.
JS
const isDarkMode = true;
const theme = isDarkMode ? "dark-theme" : "light-theme";

• Template Literals ({..})– Combines variable strings (great for ClassNames)
JS
const className = `btn ${isActive ? "btn-active" : "btn-disabled"}`;

### 5. Spread Operator (...) - shallow copying

React state is immutable (can't modify directly). You must create a copy of arrays or objects to update them.
• Copying Objects/Arrays – Spreads existing values into a new shell.
JS
const originalUser = { name: "Bob", role: "User" };
// Creates a brand new object, keeping old data but overriding the role
const updatedUser = { ...originalUser, role: "Admin" }; 



Functional React JavaScript Cheat Sheet


1. Array Methods (The Rendering Engines)

• .map(): Transforms data arrays into lists of JSX components.
• .filter(): Removes elements from lists by checking them against conditions.

2. Destructuring (The Component Pipeline)

• Object Destructuring: Extracts properties out of the props object directly into local variables.
• Array Destructuring: Extracts items sequentially by their index position, which is how useState unpacks state.

3. Arrow Functions & Implicit Returns

• Implicit Returns: Drops curly braces {} and the return keyword for cleaner, single-line functional components.

4. Template Literals & Logical Operators

• Logical AND (&&): Shortcuts conditional rendering to show JSX only when a condition matches true.
• Ternary Operator (? :): Evaluates quick inline inline if/else logic for styling or text swap states inside JSX.
• Template Literals: Injects dynamic JavaScript variables smoothly into unified string configurations like CSS class names.

5. Spread Operator (...)

• Shallow Copying: Creates exact duplicates of data objects and state arrays to respect React's immutability requirements during state updates.

Destructuring and .map() working together

import React from "react"

// 1. CONCEPT ONE: DESTRUCTURING
// Instead of accepting '(props)' and writing 'props.name', 
// we unpack/destructure 'name', 'price', and 'isAvailable' in the function arguments.

function ProductCard({ name, price, isAvailable }) {
    return (
        <div className="product-card">
            <h3>{name}</h3>
            <p>Price: ${price}</p>
            {/* Using the short-circuit && operator from the cheat sheet */}
            {!isAvailable && <p className="sold-out">Sold Out!</p>}
        </div>
    )
}

export default function ProductList() {
    // Raw JavaScript array of objects (simulating data from an API)
    const productsData = [
        { id: 101, name: "Wireless Mouse", price: 29.99, isAvailable: true },
        { id: 102, name: "Mechanical Keyboard", price: 89.99, isAvailable: false },
        { id: 103, name: "4K Monitor", price: 299.99, isAvailable: true }
    ]

    // 2. CONCEPT TWO: THE .MAP() METHOD
    // We loop over the raw data array and transform each object into a <ProductCard /> component.
    const productComponents = productsData.map((product) => {
        return (
            <ProductCard 
                key={product.id} // React needs a unique 'key' for lists
                name={product.name}
                price={product.price}
                isAvailable={product.isAvailable}
            />
        )
    })

    // Finally, we just inject the array of components directly into our JSX layout
    return (
        <section className="products-container">
            <h2>Our Store Products</h2>
            <div className="products-grid">
                {productComponents}
            </div>
        </section>
    )
}



