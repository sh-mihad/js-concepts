# JS this, call(),apply(),bind() Method

## this

জাভাস্ক্রিপ্টে this এর প্রোয়োজন হলো এটি একটা ফাংশন কে ডিফারেন্ট  কন্টেক্সকে  রি-ইউজ করতে হেল্প করে । 

JS এ this এর ৪ টি নিয়ম রয়েছে

- implicit binding / পরোক্ষ বাইন্ডিং
- Explicit Binding / প্রতোক্ষ্য বাইন্ডিং
- New Binding
- Window Binding

### implicit binding / পরোক্ষ বাইন্ডিং

কোনো ফাংশন বা মেথড যদি কোনো অব্জেক্ট এর সাথে “.” ডট নোটেশন দিয়ে ইনভোক বা কল করা হয় তাকে implicit binding বলা হয়। যেমনঃ

```jsx
// example -1 

const sakib = {
  name:"sakib",
  age:21,
  play:function(){
  console.log(this.name + " is playing")
}
}
sakib.play() // sakib is playing

// example-2
function playFn(){
  console.log(this.name + " is playing")
}
const sakib = {
  name:"sakib",
  age:21,
  play:playFn
}
sakib.play() // sakib is playing
```

উপরের কোডে playFn কে ইনভোক বা কল করা হচ্ছে sakib অব্জেক্ট দ্বারা তাই playFn এর ভিতরে this হবে sakib অব্জেক্ট । 

### Explicit Binding / প্রতক্ষ্য বাইন্ডিং

Explicit binding বলতে বুঝানো হয় কোনো ফাংশনে this কি হবে তা সরাসরি বলে দেয়া। আমরা যদি উপরের কোডটুকু একটু লক্ষ্য করি তাহলে দেখতে পাবো যে, sakib অব্জেক্ট এর ভিতরে play নামে একটি মেথড রয়েছে যা playFn কে পয়েন্ট করা হয়েছে  তাই playFn এর ভিতরে this হবে sakib ফাংশনটি। এখান যদি এমন কেইস হয় যেখানে আমাদের কোনো বাইরের ফাংশনকে কোনো অব্জেক্ট এর মেথড হিসেবে ব্যাবহার করতে হবে এবং সেই অব্জকেটের ভিতরে কোনো মেথড থাকবে না সেই ক্ষেত্রে আমরা explicit binding ব্যবহার করতে পারি। যেমন উপরের sakib অব্জকেট এর ভিতরে play নামে একটা মেথড রয়েছে যা palyFn কে রেফার করে আছে ।  এখন আমি যদি চাই যে আমি playFn কে ব্যবহার করবো play প্রোপার্টি ছাড়া তাহলে আমরা explicit binding ব্যবহার করতে পারি। যেখানে আমরা ফাংশন ইনভোক করার সময় বলে দিতে পারবো সেই ফাংশন এর this কোন অব্জকেট হবে বা সেই ফাংশন এর  this কি হবে। 

explicit binding এর জন্য ৩টি মেথড ব্যবহার করা হয় তা হলোঃ

1. call() : এটি প্রথম প্যারামিটারে একটা obj নেয় এবং এর পর থেকে ফাংশনের প্যারামিটারগুলো নেয়। অর্থাৎ যেই ফাংশন কল করতে চাচ্ছি সেই ফাংশন এর প্যারামিটার গুলো রিসিভ করে 
2. apply() : এটি প্রথম প্যারামিটারে একটা obj নেয় এবং দ্বিতীয় প্যারামিটারে একটা array নেয় যেখানে  ফাংশনের প্যারামিটারগুলো নেয়। অর্থাৎ যেই ফাংশন কল করতে চাচ্ছি সেই ফাংশন এর প্যারামিটার গুলো রিসিভ করে 
3. bind() : এটি প্রথম প্যারামিটারে একটা obj নেয় এবং এর পর থেকে ফাংশনের প্যারামিটারগুলো নেয়। অবে bind যখন কল করা হয় তখন সেটি একটি ফাংশনের ইন্সটেন্স দেয় বা ফাংশন বডি দেয় যা একটা ভ্যারিয়েবল এর ভিতরে নিতে হয় এবং সেই ভ্যারিয়েবলকে কল করে কাজ করতে হয়। 

এখন কোডের মাদ্ধ্যমে উদাহারন দেখা যাক উপরের অব্জকেট দিয়ে

```jsx
function playFn (sportsname,position){
 console.log(`${this.name} is an ${sportsname} and he is an ${position}`)
}

const sakib = {
  name:"Sakib",
  age:35
}

const messi = {
  name:"Messi",
  age:35
}

// explicit binding with call method
playFn.call(sakib,"Crickter","All Rounder") //Sakib is an Crickter and he is an All Rounder
playFn.call(messi,"Footballer","Stricker") // Messi is an Footballer and he is an Stricker

// explicit binding with apply method
playFn.apply(sakib,["Crickter","All Rounder"]) //Sakib is an Crickter and he is an All Rounder
playFn.apply(sakib,["Footballer","Stricker"]) // Messi is an Footballer and he is an Stricker

// explicit binding with bind method
const sakibPlay = playFn.bind(sakib,"Crickter","All Rounder") //Sakib is an Crickter and he is an All Rounder
const messiPlay= playFn.bind(messi,"Footballer","Stricker") // Messi is an Footballer and he is an Stricker

```

উপরের কোডে আমরা দুটি অব্জেক্ট নিয়েছি sakib & messi নামে এবং সেই অব্জকেট এর ভিতরে শুধু ২টি প্রোপার্টি আছে কোনো মেথড নেই। সেই অব্জকেট গুলো দিয়ে আমরা playFn কে ইনভোক বা কল করতে পারছি সেই অব্জকেট এর মেথড হিসেবে । playFn ফাংশন এর ভিতরে আমরা প্রত্যক্ষ ভাবে বলে দিতে পারছি সেই ফাংশন এর ভিতরে this কোন অবজেক্ট হবে বা কোন অব্জেক্টকে রেফার করবে। 

### New Binding

`new` binding হল **this** কিভাবে কাজ করে তা নির্ধারণ করার একটি নিয়ম, যা কনস্ট্রাক্টর ফাংশনের সাথে ব্যবহৃত হয়। যখন কোনো ফাংশন `new` কীওয়ার্ডের মাধ্যমে কল করা হয়, তখন নতুন একটি অবজেক্ট তৈরি হয় এবং `this` সেই নতুন অবজেক্টকে রেফার করে।

**কিভাবে `new` binding কাজ করে?**

যখন কোনো ফাংশন `new` কীওয়ার্ডের সাথে কল করা হয়, তখন নিচের ধাপগুলো ঘটে:

1. একটি নতুন ফাঁকা অবজেক্ট তৈরি হয়।
2. নতুন অবজেক্টটি `this` হিসেবে সেট হয়।
3. কনস্ট্রাক্টর ফাংশনের ভিতরের প্রোপার্টি ও মেথড নতুন অবজেক্টে সংযুক্ত হয়।
4. যদি ফাংশন এক্সপ্লিসিটভাবে কোনো অবজেক্ট রিটার্ন না করে, তাহলে নতুন অবজেক্টটি রিটার্ন হয়।

```jsx
function Person(name, age) {
    this.name = name;
    this.age = age;
}

const person1 = new Person("John", 25);
console.log(person1.name); // Output: John
console.log(person1.age);  // Output: 25
```

এখানে `new Person("John", 25)` কল করার ফলে `this` নতুন একটি অবজেক্টকে নির্দেশ করে এবং সেটির মধ্যে `name` ও `age` প্রোপার্টি যোগ হয়।

### **Window Binding**

যখন গ্লোবাল স্কোপে কোনো ফাংশন ব্যবহার করা হয় তখন সেই ফাংশন এর this হিসেবে global বা window অব্জক্টকে পয়েন্ট করে থাকে। আর তাকেই window binding বলা হয়।