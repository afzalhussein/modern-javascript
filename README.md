# Modern JavaScript (ES2023) Guide: From ES6 Foundations to Current Features

## Introduction to Modern JavaScript Evolution

JavaScript has evolved dramatically since ES6 (ES2015), with yearly ECMAScript releases bringing important improvements. This guide combines the foundational ES6 concepts with modern JavaScript (ES2023) features and best practices.

## Core Modern JavaScript Features

### 1. Variable Declarations: `let`, `const`, and `var`

```javascript
// Modern best practices:
const PI = 3.14;          // Use const by default
let counter = 0;          // Use let when reassignment is needed
// Avoid var in modern code

// Block scoping examples:
{
  const temp = 42;
  let value = 'test';
}
// temp and value are not accessible here
```

### 2. Enhanced Object Literals

```javascript
// Property shorthand
const name = 'Alice';
const age = 30;
const person = { name, age };

// Method shorthand
const calculator = {
  add(a, b) { return a + b; }
};

// Computed property names
const prop = 'key';
const obj = { [prop]: 'value' };

// Modern additions:
// Nullish coalescing in objects
const config = { timeout: userTimeout ?? 1000 };
```

### 3. Modern Destructuring

```javascript
// Object destructuring
const { id, name: userName, role = 'guest' } = user;

// Array destructuring
const [first, second, ...rest] = items;

// Function parameter destructuring
function printUser({ name, age, country = 'US' }) {
  console.log(`${name}, ${age}, ${country}`);
}

// Modern patterns:
// Nested with defaults
const { 
  settings: { darkMode = false, notifications = true } = {} 
} = userProfile;
```

### 4. Arrow Functions and `this` Binding

```javascript
// Basic form
const add = (a, b) => a + b;

// Modern usage patterns:
// Async arrow functions
const fetchData = async (url) => {
  const response = await fetch(url);
  return response.json();
};

// Immediately Invoked Arrow Functions
(() => {
  console.log('IIAF running');
})();

// Note: Arrow functions don't have their own 'this' context
```

### 5. Template Literals and String Manipulation

```javascript
// Basic interpolation
const greeting = `Hello, ${name}!`;

// Modern features:
// Tagged templates
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => 
    `${result}${str}<mark>${values[i] || ''}</mark>`, '');
}

// New string methods
const includesHello = text.includes('hello');
const startsWithHttp = url.startsWith('http');
const repeated = 'na '.repeat(3) + 'Batman!';
```

### 6. Modern Classes and Inheritance

```javascript
class Component {
  // Class fields (ES2022)
  state = {};
  #privateField = 'secret';  // Private field
  
  // Static fields
  static version = '1.0';
  
  constructor(props) {
    this.props = props;
  }
  
  // Async methods
  async loadData() {
    this.state.data = await fetchData();
  }
  
  // Private method
  #internalHelper() {
    // ...
  }
}

class Button extends Component {
  // Override field with new value
  state = { clicked: false };
  
  // Static block (ES2022)
  static {
    console.log('Button class initialized');
  }
}
```

### 7. Modern Collections: Map, Set, WeakMap, WeakSet

```javascript
// Map examples
const userMap = new Map();
userMap.set(user1, preferences1);
userMap.get(user1);

// Set examples
const uniqueTags = new Set();
uniqueTags.add('javascript');
uniqueTags.add('react');

// Modern conversions
const mapToObj = Object.fromEntries(userMap);
const objToMap = new Map(Object.entries(data));

// Set operations (ES2023+ proposals)
const intersection = new Set(
  [...set1].filter(x => set2.has(x))
);
```

### 8. Modern Array Methods and Operations

```javascript
// New immutable methods (ES2023)
const sorted = array.toSorted();
const reversed = array.toReversed();
const updated = array.with(2, 'new value');

// Modern patterns:
// Array grouping (proposal)
const grouped = array.group((item) => item.category);

// FlatMap
const allTags = posts.flatMap(post => post.tags);

// Optional chaining with arrays
const firstItem = items?.[0];
```

### 9. Modern Functions and Parameters

```javascript
// Default parameters
function createUser(name, role = 'user', active = true) {
  // ...
}

// Rest parameters
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

// Named parameters pattern (using destructuring)
function drawChart({ 
  width = 400, 
  height = 300, 
  title = 'Chart' 
} = {}) {
  // ...
}
```

### 10. Modern Error Handling

```javascript
// Error chaining (ES2022)
async function processData() {
  try {
    const raw = await fetch('/data');
    return await parseData(raw);
  } catch (error) {
    throw new Error('Processing failed', { cause: error });
  }
}

// Optional catch binding (ES2019)
try {
  riskyOperation();
} catch {
  console.log('Something went wrong');
}
```

### 11. Modern Modules System

```javascript
// Named exports
export const API_URL = 'https://api.example.com';
export function fetchData() { /* ... */ }

// Default export
export default class Service { /* ... */ }

// Modern imports
import Service, { API_URL as endpoint } from './service.js';
import * as Utils from './utils.js';

// Dynamic imports
const module = await import('/modules/module.js');

// Import attributes (proposal)
import data from './data.json' with { type: 'json' };
```

### 12. Modern Asynchronous Programming

```javascript
// Async/await pattern
async function getUserPosts(userId) {
  try {
    const user = await fetchUser(userId);
    const posts = await fetchPosts(user.id);
    return { user, posts };
  } catch (error) {
    console.error('Failed:', error);
    throw error;
  }
}

// Promise combinators
const [user, posts] = await Promise.all([
  fetchUser(userId), 
  fetchPosts(userId)
]);

const result = await Promise.any([  // Returns first successful
  fetchFromPrimary(),
  fetchFromSecondary()
]);
```

### 13. Modern Iterators and Generators

```javascript
// Custom iterators
const range = {
  *[Symbol.iterator]() {
    for (let i = 1; i <= 10; i++) yield i;
  }
};

// Async generators
async function* asyncGenerator() {
  yield await fetchPage(1);
  yield await fetchPage(2);
}

// Modern consumption
for await (const data of asyncGenerator()) {
  process(data);
}
```

### 14. Modern Number and Math Features

```javascript
// Numeric separators (ES2021)
const billion = 1_000_000_000;
const bytes = 0b1010_0101_1111;

// BigInt (ES2020)
const huge = 123456789012345678901234567890n;
const bigResult = huge * 2n;

// New Math methods
Math.clamp(value, min, max);  // Proposal
Math.degrees(radians);        // Proposal
```

### 15. Modern Regular Expressions

```javascript
// Named capture groups (ES2018)
const regex = /(?<year>\d{4})-(?<month>\d{2})/;
const { groups: { year, month } } = regex.exec('2023-05');

// Unicode property escapes (ES2018)
const emojiRegex = /\p{Emoji}/u;

// Match indices (ES2022)
const match = regex.exec('test');
console.log(match.indices);
```

### 16. Modern Object Manipulation

```javascript
// Object.hasOwn (ES2022)
Object.hasOwn(object, 'property');

// Object.groupBy (proposal)
const grouped = Object.groupBy(items, item => item.category);

// Deep cloning
const deepClone = structuredClone(obj);  // ES2022
```

### 17. Modern JSON Features

```javascript
// JSON modules (proposal)
import data from './data.json' with { type: 'json' };

// JSON.parse improvements
const obj = JSON.parse(jsonString, (key, value) => {
  if (key === 'date') return new Date(value);
  return value;
});
```

### 18. Modern Browser APIs Integration

```javascript
// Web Workers with modules
const worker = new Worker('./worker.js', { type: 'module' });

// Top-level await in modules
const analytics = await import('./analytics.js');
```

## Key Modern JavaScript Patterns

1. **Optional Chaining**: Safely access nested properties
   ```javascript
   const street = user?.address?.street;
   ```

2. **Nullish Coalescing**: Provide defaults for null/undefined
   ```javascript
   const limit = config.maxItems ?? 10;
   ```

3. **Logical Assignment**: Combine operations
   ```javascript
   user.role ||= 'guest';
   items.length &&= items.length;
   ```

4. **Pipeline Operator (Proposal)**: Functional-style chaining
   ```javascript
   const result = value |> double |> increment |> format;
   ```

5. **Pattern Matching (Proposal)**: Powerful conditional logic
   ```javascript
   match (response) {
     when { status: 200, body } -> process(body)
     when { status: 404 } -> showNotFound()
     else -> handleError()
   }
   ```

## Modern JavaScript Tooling

1. **Package Managers**: npm, yarn, pnpm
2. **Build Tools**: Vite, esbuild, Rollup, Webpack
3. **Testing**: Vitest, Jest, Playwright
4. **Linting/Formatting**: ESLint, Prettier
5. **Type Systems**: TypeScript, JSDoc
6. **Runtimes**: Node.js, Deno, Bun

## Migration Tips from ES6 to Modern JavaScript

1. Replace `var` with `let`/`const`
2. Convert promise chains to async/await
3. Use optional chaining instead of nested checks
4. Adopt nullish coalescing for default values
5. Utilize class fields and private members
6. Replace `function` with arrow functions where appropriate
7. Use modern array/object methods
8. Adopt native modules over bundlers where possible

This comprehensive guide bridges the gap between ES6 and modern JavaScript, providing a complete picture of the language's evolution while maintaining backward compatibility with ES6 concepts. The JavaScript ecosystem continues to evolve, but these modern features represent stable, widely-supported improvements to the language.
