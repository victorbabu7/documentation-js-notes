

# documentation-js-notes
JS learning notes, Parcel Point project documentation and the technologies used.


## INTRODUCTION

This repository is my personal learning journal as I grow from JavaScript beginner to full-stack developer.
I am currently learning JavaScript using a structured book, and I am now on Chapter 12. At the same time, I am working on a real project called ParcelPoint — a smart locker management system built with Next.js, React, Prisma, and Go.

The challenge I faced was simple: the project uses technologies I had not fully learned yet. So I made a plan.

> Learn JavaScript properly from the beginning → understand each concept deeply → then go back to the ParcelPoint project and see exactly how that concept is used in a real application.

Step by step, chapter by chapter, I am building a bridge between what I learn in my book and how it is applied in a professional project. This file documents that entire journey — from the very first JS concept to a full understanding of the ParcelPoint architecture.

---

## PLAN

- 1. Getting Started with JavaScript, React, Next.js
- 2. JavaScript Essentials (Variables, Operators, Data Types)
- 3. Multiple Values (Arrays, Objects) and Logic Statements (if/else, switch)
- 4. Loops (while, for, for of)
- 5. Functions (Arrow functions, Callbacks)
- 6. Classes (OOP, Inheritance)
- 7. Built-In Methods (.map(), .filter(), .reduce())
- 8. The DOM (Selecting elements)
- 9. Dynamic Element Manipulation
- 10. Interactive Content and Event Listeners

---

## Part 1 : Getting Started with JavaScript, React, Next.js

### a. JavaScript

JavaScript is a programming language that can be used on both the server side and client side in the browser of applications.

I discovered that to code effectively, I must set up an environment with a code editor like Visual Studio Code and a modern browser, for example Chrome, Firefox.

If I want to display a message I use `console.log()`, `console.table()` for visualizing structured data, and `console.error()` to report errors.

```javascript
console.log("hello victor");
console.table("");
```

If I want to integrate JS on my HTML file, I have two ways :
- Directly in HTML file between `<script>` tags
- Or by linking an external JavaScript file — which I consider the best practice.

---

### 1.1 Connection to my ParcelPoint project

My ParcelPoint project is written in Next.js, which is a framework based on React. React is a JavaScript library — so everything I learn in JavaScript is directly used in this project. Next.js organizes the code into `page.tsx` files, each file represents one page of the application, exactly like an external JavaScript file linked to an HTML page.

In my project, I have a separate file for each feature :
- In the **transactions page**, I have a `page.tsx` file that handles all the payment display.
- In the **profile page**, I have a `page.tsx` file that manages the user information.
- In the **users page**, I have a `page.tsx` file that displays the list of all users.

In the **transactions page**, I used `console.error()` to display an error when the API call fails :
```
console.error("Erreur transactions:", err);
console.warn("Erreur serveur sur l'URL :", url);
```

In the **profile page**, I used `const` to store the user token :
```
const token = localStorage.getItem('token');
```



## Part 2 : JavaScript Essentials (Variables, Operators, Data Types)

I learned how to create variables using `let`, `var` and `const`. A variable is like a box where I store information to use later in my code. I understood that `const` is for values that never change, and `let` is for values that can change. I also discovered data types : text (`String`), numbers (`Number`), booleans (`Boolean`), and empty values (`null` and `undefined`). Finally, I learned operators — arithmetic to do calculations, comparison to compare values, and logical to combine conditions.

---

### 2.1 Connection to my ParcelPoint project

In the **transactions page**, I used `const` to store the user token :
```
const token = localStorage.getItem('token');
```

In the **coupons page**, I used `let` to store the search state :
```
const [searchTerm, setSearchTerm] = useState("");
```

In the **bookings page**, `booking_id` and `owner_phone_no` are String values :
```
b.booking_id?.toLowerCase().includes(searchTerm.toLowerCase())
b.owner_phone_no?.includes(searchTerm)
```

In the **transactions page**, `amount` is a Number. I use `parseFloat()` to convert it before doing a calculation :
```j
const total = transactions.reduce((acc, curr) => 
  acc + parseFloat(String(curr.amount || 0)), 0
);
```

In the **coupons page**, `reserved` is a Boolean — either `true` or `false` :
```
reserved: false
{coupon.reserved ? 'Yes' : 'No'}
```

In the **coupons page**, `redeemed_at` can be `null` — which means the coupon has not been used yet :
```
redeemed_at: string | null;
const isRedeemed = c.redeemed_at !== null;
```

When a user logs in, their token is stored in `const` because it does not change. When they type in the search bar, the text is stored in `let` because it changes with every letter. When a parcel is delivered, its status is a `Number` — `0` means active, `1` means collected, `2` means discarded. When a coupon has not been used yet, its redemption date is `null`. When a coupon is reserved or not, it is a `Boolean` — `true` or `false`.

---

## Part 3 : Multiple Values (Arrays and Objects) and Logic Statements

### Arrays and Objects

An array is an ordered list of values. An object is a collection of named properties. I also learned array methods like `.push()`, `.filter()`, `.find()`, and I discovered that you can put objects inside arrays and arrays inside objects.

```
let fruits = ["apple", "banana", "mango"];

let parcel = {
  id: "ABC123",
  status: 0,
  locker_id: 3
};
```

In the **transactions page**, I store the list of all transactions in an array. Each transaction is an object inside that array :
```
const [transactions, setTransactions] = useState<Transaction[]>([]);
```

In the **coupons page**, each coupon is an object with multiple properties :
```
interface Coupon {
  id: number;
  coupon_code: string;
  discount_percentage: number;
  expires_at: string;
  reserved: boolean;
}
```

---

### Logic Statements

I learned how to make decisions in my code using `if`, `else if` and `else`. I also learned `switch` to handle multiple possible cases, and the ternary operator to write a short condition in one single line.

In the **transactions page**, I use a `switch` to display the right color and text depending on the transaction status :
```
switch(status) {
  case 0: return { label: 'Success', color: 'text-emerald-500' };
  case 1: return { label: 'Pending', color: 'text-amber-500' };
  case 2: return { label: 'Failed', color: 'text-rose-500' };
}
```

In the **bookings page**, I use the ternary operator to display `ACTIVE` or `EXPIRED` :
```
{b.status === 0 ? 'ACTIVE' : 'EXPIRED'}
```

---

## Part 4 : Functions

I learned that a function is a block of code that I can reuse as many times as I want. Instead of writing the same code multiple times, I write it once in a function and call it when I need it.

**Basic function :**
```
function add(x, y) {
  return x + y;
}
add(3, 5);
```

**Arrow function** — the modern syntax used in React and Next.js :
```
const add = (x, y) => x + y;
```

**Default parameters :**
```
function greet(name = "victor") {
  return "Hello " + name;
}
greet();        // "Hello victor"
greet("Babu"); // "Hello Babu"
```

---

### Function in JS vs Function in React

A simple JS function receives data, does something, and returns a result. But in React, a function can return HTML — this is called a **component**. It is a normal function but instead of returning text or a number, it returns what will be displayed on the screen. This is the big difference between React and classic JavaScript.

In my ParcelPoint project, every page is a function. For example, the transactions page is a big function called `TransactionsPage` that returns everything displayed on the screen.

In the **transactions page**, I use an arrow function `fetchTransactions` to fetch data from the API :
```
const fetchTransactions = async () => {
  const token = localStorage.getItem('token');
  const res = await fetch(url, {
    headers: { 'Authorization': `Bearer ${token}` }
  });
};
```

In the **coupons page**, I use an arrow function as a callback inside `.filter()` :
```javascript
const filtered = coupons.filter(c => {
  return c.coupon_code?.toLowerCase().includes(searchTerm.toLowerCase());
});
```

In the **bookings page**, the function `BookingsPage` is a React component — a function that returns HTML :
```
export default function BookingsPage() {
  return (
    <Layout>
      <BookingsContent />
    </Layout>
  );
}
```

Functions are the base of my entire ParcelPoint project. Every page, every action, every calculation is done by a function. In classic JavaScript a function returns data, but in React a function can directly return what is displayed on the screen. This is what makes React so powerful.

---

## Part 5 : Classes (OOP, Inheritance)
```
