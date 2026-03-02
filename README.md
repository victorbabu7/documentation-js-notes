

# documentation-js-notes
JS learning notes, Parcel Point project documentation and the technologies used.


## INTRODUCTION

This repository is my personal learning journal as I grow from JavaScript beginner to full-stack developer.
I am currently learning JavaScript using a structured book, and I am now on Chapter 12. At the same time, I am working on a real project called ParcelPoint — a smart locker management system built with Next.js, React, Prisma, and Go.

The challenge I faced was simple: the project uses technologies I had not fully learned yet. So I made a plan.

Learn JavaScript properly from the beginning → understand each concept deeply → then go back to the ParcelPoint project and see exactly how that concept is used in a real application.

Step by step, chapter by chapter, I am building a bridge between what I learn in my book and how it is applied in a professional project. This file documents that entire journey — from the very first JS concept to a full understanding of the ParcelPoint architecture.


# PLAN

1. Getting Started with JavaScript, React, Next.js
 2. JavaScript Essentials (Variables, Operators, Data Types)
 3. Multiple Values (Arrays, Objects) and Logic Statements (if/else, switch)
 4. Loops (while, for, for of)
 5. Functions (Arrow functions, Callbacks)
 6. Classes (OOP, Inheritance)
 7. Built-In Methods (.map(), .filter(), .reduce())
 8. The DOM (Selecting elements)
 9. Dynamic Element Manipulation
 10. Interactive Content and Event Listeners

# Part 1 : Getting Started with JavaScript, React, Next.js

# a. JavaScript

JavaScript is a programming language that can be used on both the server side and client side in the browser of applications.

I discovered that to code effectively, I must set up an environment with a code editor like Visual Studio Code and a modern browser, for example Chrome, Firefox.

If I want to display a message I use console.log(), console.table() for visualizing structured data, and console.error() to report errors.

javascript
console.log("hello victor");
console.table("");

If I want to integrate JS on my HTML file, I have two ways :
- Directly in HTML file between <script> tags
- Or by linking an external JavaScript file — which I consider the best practice.


### 1.1 Connection to my ParcelPoint project

My ParcelPoint project is written in Next.js, which is a framework based on React. React is a JavaScript library , so everything I learn in JavaScript is directly used in this project. Next.js organizes the code into `page.tsx` files, each file represents one page of the application, exactly like an external JavaScript file linked to an HTML page.


## Part 2 : JavaScript Essentials(Variables, Operators, Data Types)

I learned how to create variables using let, var and const. A variable is like a box where I store information to use later in my code. I understood that const is for values that never change, and let is for values that can change. I also discovered data types : text (String), numbers (Number), booleans (Boolean), and empty values (null and undefined). Finally, I learned operators  arithmetic to do calculations, comparison to compare values, and logical to combine conditions.


# 2.1 Connection to my ParcelPoint project
for exemple 
In the **transactions page**, I used const to store the user token :

const token = localStorage.getItem('token');


# Part 3 : Multiple Values (Arrays and Objects) and Logic Statements

#Arrays and Objects

An array is an ordered list of values. An object is a collection of named properties. I also learned array methods like .push(),filter(), .find(), and I discovered that you can put objects inside arrays and arrays inside objects.

let fruits = ["apple", "banana", "mango"];

let parcel = {
 id: "ABC123",
 status: 0,
 locker_id: 3
};


In the **transactions page**, I store the list of all transactions in an array. Each transaction is an object inside that array :
const [transactions, setTransactions] =useState<Transaction[]>[];

In the **coupons page**, each coupon is an object with multiple properties :

interface Coupon {
  id: number;
  coupon_code: string;
  discount_percentage: number;
  expires_at: string;
  reserved: boolean;
}


# Logic Statements

I learned how to make decisions in my code using if, else if and else. I also learned switch to handle multiple possible cases, and the ternary operator to write a short condition in one single line.

In the **transactions page**, I use a switch to display the right color and text depending on the transaction status :
switch(status) {
  case 0: return { label: 'Success', color: 'text-emerald-500' };
  case 1: return { label: 'Pending', color: 'text-amber-500' };
  case 2: return { label: 'Failed', color: 'text-rose-500' };
}
In the **bookings page**, I use the ternary operator to display ACTIVE or EXPIRED :
{b.status === 0 ? 'ACTIVE' : 'EXPIRED'}

# Part 4 : Functions

I learned that a function is a block of code that I can reuse as many times as I want. Instead of writing the same code multiple times, I write it once in a function and call it when I need it.

**Basic function :**

function add(x, y) {
  return x + y;}
add(3, 5);

**Arrow function** — the modern syntax used in React and Next.js :

const add = (x, y) => x + y;
**Default parameters :**
function greet(name = "victor") {
 return "Hello " + name;}
greet();         
greet("Babu");  

# Function in JS vs Function in React

A simple JS function receives data, does something, and returns a result. But in React, a function can return HTML — this is called a **component**. It is a normal function but instead of returning text or a number, it returns what will be displayed on the screen. This is the big difference between React and classic JavaScript.

In my ParcelPoint project, every page is a function. For example, the transactions page is a big function called Transactions page that returns everything displayed on the screen.

In the **transactions page**, I use an arrow function fetchTransactions to fetch data from the API :

const fetchTransactions = async () => {
 const token = localStorage.getItem('token');
 const res = await fetch(url, {
headers: { 'Authorization': Bearer ${token}` }});
};

In the **coupons page**, I use an arrow function as a callback inside .filter()` :

const filtered = coupons.filter(c => {
  return c.coupon_code?.toLowerCase().includes(searchTerm.toLowerCase());
});


In the **bookings page**, the function BookingsPage is a React component , a function that returns HTML :

export default function BookingsPage() {
  return (
   <Layout>
   <BookingsContent />
    </Layout>
  );
}

Functions are the base of my entire ParcelPoint project. Every page, every action, every calculation is done by a function. In classic JavaScript a function returns data, but in React a function can directly return what is displayed on the screen. This is what makes React so verry important .

## Part 6 : Classes (OOP, Inheritance)
I discovered that classes are essentially models for creating objects. 

Here are the technical concepts I learned :

The Constructor: this is the special method I use to initialize my objects. It runs automatically as soon as I use the new keyword.
The this keyword  : I use it to refer to the specific instance of the object I am creating or working with.

Methods:these are functions defined directly inside the class, without the function keyword, that allow my objects to perform actions.

Encapsulation : I learned how to protect my data by using the # symbol before a property name, for example #nom, to make it private. To read or modify this data safely, I use getters and setters.

Inheritance with extends — I can create a child class that inherits all the properties and methods of a parent class. In this case, I must call super()  in the child constructor to initialize the parent.

**exemple**


In my book, i learned that the constructor of a class defines what properties an object must have :

class Parcel {
constructor(id, parcelid, statu) {
this.id = id;
this.parcel_id = parcel_id;
this.status = status}}


in my project, the interface does exactly the same thing , just Same idea, just written differently.

interface Parcel {
id: number;
parcel_id: string;
status: number}

Im book , i learned that a child class inherits from a parent class using extends.
ParcelStats is like a child  , it does not repeat all the parcel information.

In my book, i learned that encapsulation means hiding data inside a class using #.
In my project, setStats stores the data inside the component. Nobody from outside can modify it directly.

**7. Built-In Methods (.map(), .filter(), .reduce())**

on my book ,  see the signification : 
map() : transforms each value in an array and creates a new one.
.filter(): keeps only the elements that match a condition.
.reduce() :combines all values into one single result.

in mya project, i  see .filter() and .reduce() used in my parcels page and transactions page in ParcelPoint :

active: uniqueParcels.filter(p => p.status === 0).length,
total: transactions.reduce((acc, curr) => acc + parseFloat(String(curr.amount || 0)), 0)

## Part 7 : The DOM and Dynamic Element Manipulation

The DOM is a tree representation of my HTML page. JavaScript uses it to select and modify elements in real time without reloading the page.

To select elements i use :

document.getElementById("myId")
document.querySelector(".myClass")
document.querySelectorAll("p")

To modify elements i can change the text, the style, the classes or create new elements :

element.innerText = "bonjour";
element.style.backgroundColor = "red";
element.classList.toggle("isopen");

In ParcelPoint project, React does this automatically for me.
Instead of selecting elements manually, i just change a state variable and React updates the page :

const [loading, setLoading] = useState(true);
{loading ? <Loader2 className="animate-spin" /> : <div>{parcels}</div>}

Instead of classList.add(), i define classes dynamically based on data :

className={user.active ? 'text-emerald-500' : 'text-red-500'}

React is built on top of the DOM , it does the same thing but faster and automatically.

##Interactive Content and Event Listeners
 

I learne that an event is an action that happens on the page  ,a click, a key press, a mouse movement.I can listen to these actions and run code when they happen.

In classic JavaScript i use addEventListener to listen to events :
document.getElementById("btn").addEventListener("click", myFunction);


In React i don't need addEventListener anymore. 
I write the event directly in the component :
<button onClick={myFunction}>Click me</button>

I also learne event.target.value to get what a user types in an input field.
In React it works exactly the same way.

I can see both concepts used in my ParcelPoint project.

In my parcels page, i use onClick to sync the data when the button is clicked :

<button onClick={fetchParcels}>
  Sync Data
</button>

In my bookings page, i use onChange and event.target.value to get what the user types in the search bar :
<input
  onChange={(e) => setSearchTerm(e.target.value)} />

In classic JavaScript i manage events manually. In React i just write onClick or onChange directly in the component and React handles everything automatically.


# b. React 
   
   1. JSX, rendering, components, props)
      -----------------------------------
a. JSX is a special syntax that allows me to write HTML directly within JavaScript.
   Without JSX, I would have to create each element manually in JavaScript. With JSX, I simply write the HTML and JavaScript together in the same file, making the code much easier to read and write.
   With JSX, I simply write the HTML and JavaScript together in the same file, making the code much easier to read and write.
   
b. rendering :  This is when React determines what needs to change on the screen. When I modify something, React compares the old version of the component with the new one and only updates the parts that have actually changed to remain ultra-fast. And in my parcelpoint  project, I use this method . 

c. Props : Props are like arguments that you pass to a function. They allow you to send information from a parent component to a child component.

