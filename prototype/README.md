# Prototype and Prototype Inheritance

JS হচ্ছে প্রোটোটাইপ বেইজড ল্যাঙ্গুয়েজ। জাভাস্ক্রিপ্ট এর সব কিছুই অব্জেক্ট। আর এই অব্জেক্ট এর সাথে জড়িয়ে আছে প্রোটোটাইপ কন্সেপ্ট। prototype হচ্ছে ফাংশ এর প্রোপার্টি যা একটা অব্জেক্ট কে পয়েন্ট করে 

prototype হচ্ছে ফাংশন এর একটা বিল্ট ইন প্রোপার্টি যেটা জাভাস্ক্রিপ্ট আমাদের দেয়। সেই prototype এর মধ্যে আমি চাইলে যেই যেই জিনিস গুলো শেয়ার করা প্রোয়োজন সেই জিনিস গুলো আমরা রাখতে পারি এবং তা শেয়ার করতে পারি। অর্থাৎ, প্যারেন্ট এর কোনো জিনিস যদি চাইল্ড এ শেয়ার করতে হয় সেটা প্রোটোটাইপের মাধ্যমে করা হয়ে থাকে। এটা OOP এর প্রোটোটাইপ ইনহেরিটেন্স এর কাজ করে থাকে। জে এস এ প্রোটোটাইপের মাধ্যেম প্যারেন্ট থেকে চাইল্ডএ ইনহেরিট করে নিয়ে আসে। 

### constructor ফাংশনঃ

constructor  ফাংশন programming এর একটি স্পেশাল টাইপের ফাংশন যেটা দিয়ে অব্জেক্ট এর রেপ্লিকা তৈরি করা হয়। এই ফাংশন থেকে কোনো কিছু return করা লাগে না সে নিজে নিজে একটা অব্জেক্ট রিটার্ন করে থাকে । আর এই ফাইংশন ব্যবহার করে অব্জকেট তৈরি করতে হলে new কি ওয়ার্ড ব্যবহার করতে হয়।  

যেমনঃ 

```jsx
 function Person(name,age){
 this.name = name
 this.age = age
 this.play = function(){
 console.log(this.name + "is playing")
 }
 }
 
 const sakib = new Person("sakib",34)  // output- sakib={name:"sakib",age:34,play:func}
 const tamim = new Person("tamim",32)  // output- tamim={name:"tamim",age:32,play:func}
```

উপরেরে কোডে যদি আমরা খেয়াল করি তাহলে দেখতে পাবো Person কন্সট্রাক্টর ফাংশন এর সাহায্যে অব্জেক্ট তৈরি করতে পারি। তবে সেখানে play নামের একটা জেনেরিক ফাংশন আছে যার কাজ সবঅব্জেক্ট এর ক্ষেত্রে সেইম। যেহেতু ফাংশন আলাদা একটা অব্জক্ট তাই person দিয়ে তৈরি করা অব্জকেট আলাদা করে play নামের ফাংশন তৈরি করছে এবং প্রতিটি অব্জকেট এর জন্য আলাদা আলাদা মেমোরি তে জায়গা দখল করতেছে। আর এই কাজটিকে prototype এর মাধ্যমে অনেক সহজ করা যেতে পারে যেখানে একটা মেমোরি রেফারেন্স দিয়ে সবগুলো অব্জক্টে পাস করা যেতে পারে যেমনঃ

```jsx
 function Person(name,age){
 this.name = name
 this.age = age
 }

Person.prototype.play = function(){
  console.log(this.name+" is playing")
}
 
 const sakib = new Person("sakib",34) //output - sakib={name:"sakib",age:34}
 const tamim = new Person("tamim",32) //output - tanun={name:"tamim",age:32}
 tamim.play() // output- tamim is playing
```

এখানে prototype এর সাহায্যে play ফাংশন একটি জায়গায় মেমোরি এলোকেট হয়েছে এবং তা সকল অব্জক্টের সাথে শেয়ার করা যাচ্ছে। সেই ক্ষেত্রে sakbi এবং tamim অব্জকেটের প্রোপারটী 2 টা name & age কিন্তু Person ফাংশন এর prototype এর সাহায্যে play ফাংশন এক্সেস করা যাচ্ছে। 

তাহলে prototype হচ্ছে ফাংশন এর একটি বিল্টিন প্রোপার্টি যা একটি অব্জেক্টকে পয়েন্ট করে থাকে। আর সেই ফাংশন দিয়ে যা তৈরি করা হয় সেইখানে prototype এর ভ্যালু এক্সেসেবল থাকে যেটা আমরা উপরে দেখেছি।  JS এ এই prototype inheritance এর সাহায্যে ক্লাস ব্যবহার করা যায়। 

### Prototype Chain:

prototype chain বলতে বুঝায় প্যারেন্ট prototype থেকে কোনো কিছুকে এক্সেস করাকে বুঝায়। আমরা জানি জাভাস্ক্রিপ্টে সব কিছু object আর এই object তৈরি হয় মাস্টার অব্জেক্ট থেকে যা Object নামে থাকে। আমরা যখন কোনো ফাংশন তৈরি করি তখন সেটাকে যদি আমরা console.dir(fnc) করি তখন দেখতে পাবো fnc এর নিজেস্ব prototype থাকে আবার সেই ফাংশন fn  prototype এর এক্সেস পেয়ে থাকে আবার fn মাস্টার Object এর prototype থেকে আসে। এইভাবে এক্সেস করাকে prototype chain বলে। 

```jsx
function fnc(){}
console.dif(fnc)
--------------//output-----
arguments:null
caller:null
length:0
name:"Person"
prototype:{}
[[Prototype]]:ƒ () // exapnd করলে তার নিজেসব প্রোপারট্টি & মেথড পাবো এবনং Object prototype পাবো 
     [[Prototype]]:Object
```

আমরা চাইলে মাস্টার অব্জেক্টে আমাদের নিজেসব প্রোপার্টি  বা মেথড add করতে পারবো যেমনঃ

```jsx
Object.prototype.myName = function(){
  console.log("My name is sabbir")
}

const p ={}
p.myName() //output- My name is sabbir
```

### Prototype Inheritance:

prototype inheritance বলতে বুঝায় একটা ফাংশন এর prototype আরেকটি ফাংশনের সাথে শেয়ার করা 

নিচে একটি উদাহারন দেখা যাকঃ 

```jsx
function Person (name,age){
    this.name = name;
    this.age = age
}

Person.prototype = {
    eat:function(){
        console.log(`${this.name} is eating`);
    }
}

function Cricketer(name,age,type,country){
    Person.call(this,name,age)
    this.type = type;
    this.country = country
}

Cricketer.prototype = Object.create(Person.prototype)

const sakib = new Cricketer("sakib",23,"allrounder","ban")
```

উপরের কোডে Person কোনস্ট্রাক্টরটি এবং Cricketer কোনস্ট্রাক্টরটি  আলাদা আলাদা অব্জকেট রিটার্ন করে। এখানে  sakib আগে একজন পারসন তারপর ক্রিকেটার ।এখানে আমরা চাচ্চি দুটি কোন্সট্রাকটর ফাংশনকে এক সাথে করে একটা নতুন অব্জেক্ট তৈরি করা। যেহেতু sakib আগে একজন পারসন পরে criketer তাই Person কন্সট্রাক্টর ফাংশনটি হবে প্যারেন্ট এবং  Cricketer কন্সট্রাক্টর ফাংশনটি হবে  চাইল্ড।  তাই Cricketer কন্সট্রাক্টর ফাংশনে Person কন্সট্রাক্টরটি ইনহ্যেরিট করবে এবং Cricketer ফাংশনের  prototype ,  Person ফাংশন এর prototype কে inherit করবে। 

আর এইভাবে prototype inheritance এর মাদ্ধ্যমে জাভাস্ক্রিপ্টি class inheritance  কাজ করে। পিউর জাভাস্ক্রিপিটে class নাই তবে es6 এর পরে js class নিয়ে এসেছে যা সিন্টেক্টিকালি সুগার দেয়। 

উপরের কোডকে যদি আমরা JS এর ক্লাস দ্বারা কনভার্ট করি তাহলে, 

```jsx
class Person{
    constructor(name,age){
    this.name = name
    this.age = age
    }
    eat(){
     console.log(`${this.name} is eating`)
    }
  }
  
  class Cricketer extends Person{
   constructor(name,age,type,country){
    super(name,age)
    this.type = type;
    this.country = country
   }
   play(){
    console.log(`${this.name} is playing`)
   }
  }

  const sakib = new Cricketer("sakib",34,"allrouner","ban")
```