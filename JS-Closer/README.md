# JS-Closer

ক্লোজার মানে হচ্ছে বন্ধনি বা জড়িয়ে ধরে রাখা অথবা মনে রাখা । এক কথায় কোনো ফাংশন তার প্যারেন্ট স্কোপ এর রেফারেন্স ধরে রাখাকে কোজার বলে। 

যেমনঃ

```jsx
var a =30
var b =20
function sum (){
  console.log(a+b) // ekhane global scope er refarence rakhai hocche closer
}

// sum()

console.dir(sum) // jodi console kori tahole scope er vitore global name ekta obj ache jekhane global scop er sob kichur ref thake
```

তবে একচুয়াল ক্লোজার বলতে বুঝায়,  একটা চাইল্ড ফাংশন যদি তার প্যারেন্ট ফাংশন এর কোনো ভ্যারিয়েবল ব্যবহার করে সে  জন্য প্যারেন্ট ফাংশনের ভেরিয়েবল কে চাইল্ড ফাংশন মনে রাখে বা সেই ভেরিয়েবল কে কোনো একটা জায়গায় স্টোর করে রাখে।  আর সেই স্টোর করে রাখাকে ক্লোজার বলে।  

যেমনঃ 

```jsx
var a =10
function parentFunc(){
var b = 20  // colser variable
return function(){
 return a+b
}
}

var getSum = parentFunc()

console.dir(getSum)
```

এখানে b ভেরিয়েবল হচ্ছে ক্লোজার ভেরিয়েবল। 

উপরের কোড গুলোর console.dir এর রেজাল্ট দেখি তাহলে নিচের এইভাবে দখতে পাবো। 

![image.png](attachment:4cc9b079-4886-488c-a494-be13946a761c:image.png)

এখানে একটা ব্যাপার মনে রাখতে হবে। ফাংশনের ক্লোজার অব্জেক্ট এর ভিতরে ভেরিয়েবল এর ভ্যালু কে স্টোর করে না বরং সেই ভেরিয়েবল এর রেফারেন্স ধরে রাখে। অর্থাৎ, ভেরিয়েবল এর ভ্যালু যদি চেইঞ্জ হয় তাহলে সেখানে সাথে সাথে চেইঞ্জ হয়ে যাবে । 

আর ফাংশন স্কোপের বাইরে বা গ্লোবার স্কোপের মধ্যে var দিয়ে ডিক্লার করা ভেরিয়েবল গুলো Global নামের অব্জকেট এর ভিতরে থাকবে। তবে এখানে আরেকটা ব্যাপার মনে রাখতে হবে যে, let, const দিয়ে ডিক্লার করা ভেরিয়েবল গুলো গ্লোবাল এর ভিতরে থাকে না সেগুলো Script নামে একটা অব্জকেট এর ভিতরে থাকে

```jsx
let a =10
function parentFunc(){
let b = 20  // colser variable
return function(){
 return a+b
}
}

var getSum = parentFunc()

console.dir(getSum)
```

![image.png](attachment:7755cb06-ad1b-458d-9f04-7e4e9166761e:image.png)

## গারভেজ কালেকশনঃ

এখানে একটা জিনিস মনে রাখতে হবে, জাভাস্ক্রিপ্ট অটো গারভেজ কালেক্ট করে । অর্থাৎ, যখন কোনো ভ্যারিয়েবল বা ফাংশন এর এক্সিকিউশন শেষ হয়ে যায় তখন জাভাস্ক্রিপ্ট ইন্টেলিজেন্টলি সেই কমপ্লিটেড ভ্যারিয়েবল বা ফাংশন কে মেমরি থেকে মুছে ফেলে দেয় । আর এই প্রসেস কে বলা হয় গারভেজ কালেক্ট। 

তবে ক্লোজার ব্যবহার এর কারনে ফাংশনের ক্লজার ভ্যালু কে অটো গারভেরজ কালেক্ট করতে পারে না তাই প্রোগ্রামার কে ম্যানুয়ালি গারভেজ কালেক্ট করতে হয় বা সেই ক্লোজার ভ্যালু কে মেমরি থেকে মুছে ফেলতে হয় যেমনঃ 

```jsx
function parentFunc(){
  const startTime = Date.now()
  return function (){
    return Date.now() - startTime
  }
}
var timer = parentFunc()
//
for(let i= 0;i<1000;i++){
  Math.random()*1000
}

timer()
timer()
// remove timer colosure from memory
timer = null 
timer() // TypeError: timer is not a function
```