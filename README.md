# REACT-Cheat-Sheet

#### Things to Review:

###### Static Pages
1. JSX
2. Custom components

###### Data Driven Pages
3. Dynamic web apps change with UI data 
4. Component reuseability and how Props help create reuseability
5. Creating components from an array of Data using array methods
6. Import static assets

###### Interactive Pages
7. Event listeners to interact in React and update app or API's
8. State in React to maintain data between re-renders
9. Declarative React API to only change Data that changed
10. Conditional Rendering using state
11. React Forms to take data from UI and use it
12. State management and where it is held

###### Side Effects
13. Controlled components
14. React Functional programming and side effects
15. Fetching Data with React when API loads
16. Side Effects and applying them in REACT

###### React Router
17. Next.js for front end or back end
18. Node.js in back end for REST API's


### Expanded reference sheet for above sections

1. Static Pages

Building non-interactive UIs by breaking pages into reusable pieces.

Core Concepts

• JSX Rules: Use className instead of class, camelCase HTML attributes (onClick, tabIndex), and wrap adjacent elements in a single parent tag or Fragment (<>...</>).
• Custom Components: Write JavaScript functions starting with a capital letter (Header) that return JSX, then render them as <Header /> or <Header>...</Header> (using props.children).
• Modules: Split components into separate files using export default and import to keep projects organized.

Reference Pattern

jsx
export default function Header() {
    return (
        <header className="site-header">
            <img src="/logo.png" alt="Chef Claude logo" />
            <h1>Chef Claude</h1>
        </header>
    )
}
Use code with caution.

Code Review Checklist

• Capitalized component names: Do all custom component functions start with an uppercase letter?
• Single root element: Does every component return one top-level parent tag or Fragment?
• Semantic HTML: Are you using proper tags (<header>, <main>, <section>, <nav>) instead of nesting <div> tags everywhere?

2. Data-Driven React

This section replaces hardcoded markup with reusable components powered by props and arrays.

Core Concepts

• Props & Destructuring: Pass data into components like HTML attributes and unpack them cleanly in the function parameters (function Card({ title, img })).
• Transforming Arrays with .map(): Convert an array of data objects into an array of JSX elements.
• The key Prop: Provide a stable, unique identifier (key={item.id}) on the outermost element returned inside .map() so React tracks list updates accurately.

Reference Pattern

jsx
function Entry({ item }) {
    return (
        <article className="entry">
            <h2>{item.title}</h2>
            <p>{item.description}</p>
        </article>
    )
}

export default function EntryList({ entries }) {
    const entryElements = entries.map(entry => (
        <Entry key={entry.id} item={entry} />
    ))

    return <section>{entryElements}</section>
}
Use code with caution.

Code Review Checklist

• Unique keys: Are you using a real unique ID for key rather than the array index (especially when items can be added, deleted, or reordered)?
• Prop readability: If you are passing 4 or more props from a single object, are you passing the object cleanly (item={entry}) or spreading ({...entry}) intentionally?
• Pure rendering: Does your component simply display the props it receives without trying to modify them?

3. React State (Chef Claude)

This section makes apps interactive by storing dynamic data and updating the UI automatically when state changes.

Core Concepts

• useState Hook: Declare state with const [value, setValue] = useState(initialValue) and never mutate value directly.
• Functional State Updates: When the new state depends on the previous state, pass a callback (setCount(prevCount => prevCount + 1)).
• Immutable Arrays & Objects: Always create a new copy using .map(), .filter(), or the spread operator ([...prevItems, newItem]).
• Conditional Rendering: Show or hide UI based on state using {isReady && <Recipe />} or {isLoading ? <Spinner /> : <Content />}.
• Lifting & Passing State: Keep shared state in the closest common parent component, passing state values down as props and updater functions down as event callbacks.

Reference Pattern

jsx
import { useState } from "react"

export default function IngredientManager() {
    const [ingredients, setIngredients] = useState([])

    function addIngredient(formData) {
        const newIngredient = formData.get("ingredient")
        if (!newIngredient) return
        setIngredients(prev => [...prev, newIngredient])
    }

    return (
        <main>
            <form action={addIngredient}>
                <input name="ingredient" type="text" placeholder="e.g. oregano" />
                <button>Add ingredient</button>
            </form>

            {ingredients.length > 0 && (
                <ul>
                    {ingredients.map(item => <li key={item}>{item}</li>)}
                </ul>
            )}
        </main>
    )
}
Use code with caution.

Code Review Checklist

• No direct mutation: Did you avoid .push(), .pop(), or state.prop = value directly on state variables?
• Derived values vs. extra state: Did you calculate values directly during render (like const hasIngredients = ingredients.length > 0) instead of storing redundant useState variables?
• Controlled vs. FormData inputs: Are form inputs properly cleared or synced after submission?

4. Side Effects

This section connects React components to external systems like APIs, browser storage, timers, and DOM refs.

Core Concepts

• useEffect Hook: Run side-effect code after React updates the DOM so rendering stays pure and predictable.
• Dependency Array:
	• Omit array: Runs after every single render (rarely needed).
	• Empty array []: Runs once when the component first mounts.
	• Populated array [id, query]: Runs on mount and whenever any listed value changes.
• Cleanup Functions: Return a function from useEffect (return () => clearInterval(id)) to prevent memory leaks when a component unmounts.
• Refs (useRef): Store mutable values that persist across renders without triggering re-renders, or grab direct access to a DOM node (such as smooth-scrolling to a newly generated recipe).

Reference Pattern

jsx
import { useState, useEffect, useRef } from "react"

export default function MemeViewer({ memeId }) {
    const [memeData, setMemeData] = useState(null)
    const sectionRef = useRef(null)

    useEffect(() => {
        let isMounted = true

        async function fetchMeme() {
            const res = await fetch(`https://example.com{memeId}`)
            const data = await res.json()
            if (isMounted) setMemeData(data)
        }

        fetchMeme()

        return () => {
            isMounted = false
        }
    }, [memeId])

    return <section ref={sectionRef}>{memeData?.title}</section>
}
Use code with caution.

Code Review Checklist

• Complete dependency array: Is every state variable or prop used inside useEffect listed in its dependency array?
• No unnecessary effects: Are you only using useEffect to sync with external systems (APIs, localStorage, event listeners, DOM scrolling), rather than handling user button clicks (which belong in event handlers)?
• Cleanup included: Do event listeners (window.addEventListener) and timers (setInterval) have a matching cleanup return function?
Would you like to paste one of your finished project files (such as MainSection.jsx or App.jsx) for a personalized code review, or are you planning a new React project to build next?



# Functional React JavaScript. 

#### Features that Functional React relies on.

### 1. Array Methods (The Rendering Engines)

Functional React rarely uses for loops. Arrays of data transformed into arrays of JSX elements.
• .map() – For looping through data and render lists of components.
JS
const users = ["Alice", "Bob", "Charlie"];
const listItems = users.map(user => `<li>${user}</li>`);

• .filter() – Removes items from lists (like deleting a todo item).
JS
const todos = [{id: 1, text: "Clean"}, {id: 2, text: "Cook"}];
const remaining = todos.filter(todo => todo.id !== 1);    // Removes item 1

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
`const MyComponent = () => {
    return <h1>Hello</h1>;
};`

// Implicit (Automatic return - simple JSX)
`const MyComponentShort = () => <h1>Hello</h1>;`

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



