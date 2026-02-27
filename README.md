# documentation-js-notes
JS learning notes, Parcel Point project documentation and the technologies used.


                                         INTRODUCTION 


 This repository is my personal learning journal as I grow from JavaScript beginner to full-stack developer.
I am currently learning JavaScript using a structured book, and I am now on Chapter 12. At the same time, I am working on a real project called ParcelPoint — a smart locker management system built with Next.js, React, Prisma, and Go.
The challenge I faced was simple: the project uses technologies I had not fully learned yet. So I made a plan.
My plan is this:

Learn JavaScript properly from the beginning → understand each concept deeply → then go back to the ParcelPoint project and see exactly how that concept is used in a real application.

Step by step, chapter by chapter, I am building a bridge between what I learn in my book and how it is applied in a professional project. This file documents that entire journey — from the very first JS concept to a full understanding of the ParcelPoint architecture.

PLANE 

 1: Getting Started with JavaScript , react , nexjs 
 2:JavaScript Essentials (Variables, Operators, Data Types)
 3: Multiple Values (Arrays, Objects) and Logic Statements (if/else, switch)
 4:Loops (while, for, for of)
 6:Functions (Arrow functions, Callbacks)
 7: Classes (OOP, Inheritance)
 8:Built-In Methods (.map(), .filter(), .reduce())
 9: The DOM (Selecting elements)
10:Dynamic Element Manipulation
11: Interactive Content and Event Listeners


part 1 : getting started with javacript , react , nexjs 
a. javascript: 
 javaScript is a language programing that can be used on both the server side and client side  in the browser  , of applications.
 i discovered tha to code effectively , i must set up an environement with a coode edito likr visual studio cide and modern browser ,
 for exemple chrome , fire fox , ,, 
 if i want to display a message on use js , , i can use  console.log(); 
 cosole.table() for visualize  structured data , and console.error() to report errows. 
  for exemple : consol.log ("hello victor") or console.table("")
 If i want integrete js on my  html file , a have tow way : 
   a. directly in html file between <script > tags or, what i consider a best pratice , by linking an external javascript file,
   i learnend to use  relative paths to ensure my file are connectly connected .


My ParcelPoint project is written in Next.js, which is a framework based on React. React is a JavaScript library — so everything i learn in JavaScript is directly used in this project. Next.js organizes the code into page.tsx files, each file represents one page of the application, exactly like an external JavaScript file linked to an HTML page.

1.1 for my project ParcelPoint

In chapter 1, i learned that the best practice is to link an external JS file instead of writing code directly in HTML. In my project, i have a separate file for each feature :

   In the transactions page, i have a page.tsx file that handles all the payment display.
   In the profile page, i have a page.tsx file that manages the user information.
   In the users page, i have a page.tsx file that displays the list of all users.


 I learned that console.log() displays a message and console.error() reports an error. In the transactions page of my project, i can see that i used console.error() to display an error when the API call fails
 
console.error("Erreur transactions:", err);
console.warn("Erreur serveur sur l'URL :", url);


for Variables with const and let , learned that const is for values that never change and let is for values that can change. In the profile page of my project, i can see that i used const to store the user token, because this value does not change during the operation : const token = localstorage.getItem('token')

2.javaScript Essentials (Variables, Operators, Data Types)

I learned how to create variables using let, var and const. 
A variable is like a box where i store information to use later in my code. I understood that const is for values that never change, and let is for values that can change. 
I also discovered data types : text (String), numbers (Number), booleans (Boolean — true or false), and empty values (null and undefined). Finally, i learned operators — arithmetic to do calculations, comparison to compare values, and logical to combine conditions.


 How i see this in my ParcelPoint project :
1. const for values that never change

 In the transactions page of my project, i can  used const to store the user token, because this value does not change during that operation : const token = localStorage.getItem('token');
encore; 
In the coupons page, i can  used let to store the search state, because this value changes every time the user types something : const [searchTerm, setSearchTerm] = useState("");

the bookings page, i can  booking_id and owner_phone_no are String values — text : b.booking_id?.toLowerCase().includes(searchTerm.toLowerCase())
b.owner_phone_no?.includes(searchTerm)

4. Number — type nombre
Dans la page des transactions, je vois que amount est un nombre. J'utilise parseFloat() pour le convertir en nombre avant de faire un calcul :
In the transactions page,  amount is a number. I use parseFloat() to convert it into a number before doing a calculation
  const total = transactions.reduce((acc, curr) => 
  acc + parseFloat(String(curr.amount || 0)), 0
);

In the coupons page, i can see that reserved is a boolean — either true or false — to know if a coupon is reserved or not :
javascriptreserved: false   // Boolean
{coupon.reserved ? 'Yes' : 'No'}

Dans la page des coupons, je vois que redeemed_at peut être null — ce qui veut dire que le coupon n'a pas encore été utilisé :
In the coupons page, i can see that redeemed_at can be null — which means the coupon has not been used yet :
javascriptredeemed_at: string | null;
const isRedeemed = c.redeemed_at !== null;

in brief , i understood that my ParcelPoint project uses variables and data types everywhere. Every piece of information that flows through my application — the user token, the transaction amount, the parcel status — is stored in a variable with the right type.

When a user logs in to my project, their token is stored in const because it does not change. When they type in the search bar, the text is stored in let because it changes with every letter. When a parcel is delivered, its status is a Number — 0 means active, 1 means collected, 2 means discarded. When a coupon has not been used yet, its redemption date is null. When a coupon is reserved or not, it is a Boolean — true or false.

3.  Multiple Values (Arrays and Objects) and logical statement
   
when talking about multiple values, we mean an array, and an object, how to manage to store several values ​​in an array and in an object
An array is an ordered list of values. An object is a collection of named properties. I also learned array methods like .push(), .filter(), .find(), and i discovered that you can put objects inside arrays and arrays inside objects.

   let fruits = ["apple", "banana", "mango"];
   let parcel = {
  id: "ABC123",
  status: 0,
  locker_id: 3

  for  exemple in my project parcelpoint , 
  i store the list of all transactions in an array. Each transaction is an object inside that array : const [transactions, setTransactions] = useState<Transaction[]>([]);

In the coupons page, each coupon is an object with multiple properties — its code, its discount percentage, its expiration date :
interface Coupon {
  id: number;
  coupon_code: string;
  discount_percentage: number;
  expires_at: string;
  reserved: boolean;

in logical statement , 
 i learned how to make decisions in my code using if, else if and else. I also learned switch to handle multiple possible cases, and the ternary operator to write a short condition in one single line.
 
 In the transactions page, i use a switch to display the right color and text depending on the transaction status — success, pending, or failed :
switch(status) {
  case 0: return { label: 'Success', color: 'text-emerald-500' };
  case 1: return { label: 'Pending', color: 'text-amber-500' };
  case 2: return { label: 'Failed', color: 'text-rose-500' };

  , i use the ternary operator to display ACTIVE or EXPIRED depending on the booking status  in a bouking page:
javascript{b.status === 0 ? 'ACTIVE' : 'EXPIRED'} 

4. Functions (Arrow functions, Callbacks)

