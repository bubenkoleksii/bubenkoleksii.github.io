---
title: "Function overloading in TypeScript"
date: 2025-07-27 15:00:00 +0300
categories: [TypeScript]
tags: [TypeScript, Front-end]
---

## 1. Problem

<span style="color: orangered">**In JS**</span>, when the implementation of a function depends on parameters, we often have to <span style="color: orangered">**introduce the optional parameters**</span> as here. 
For example, we need to implement a function to add numbers and strings.

```javascript
function combine(input1, input2, input3 = "") // input3 is optional {
  if (typeof input1 === "number" && typeof input2 === "number") {
    return input1 + input2; // Add numbers
  } else if (typeof input1 === "string" && typeof input2 === "string") {
    return input1 + input2 + input3; // Concatenate strings
  } else {
    throw new Error("Both arguments must be either numbers or strings.");
  }
}

// Using the function
combine(10, 20); // Returns 30
combine("Hello, ", "World!"); // Returns "Hello, World!"
combine("Hello", "World", "!"); // Returns "HelloWorld!"
// console.log(combine("Hello", 10)); // Throws an error
```

As you can see, <span style="color: red">**it's not user-friendly, and it's not intuitive**</span>.

## 2. Solution in TS

Similar to C#, <span style="color: green">**TypeScript has the ability to overload methods and constructors.**</span>

But in TS we have <span style="color: magenta">**one implementation**</span> and <span style="color: magenta">**many signatures**</span>. If we pass parameters that do not match the signature, an error will occur.

You can think of it like a pizza chef who receives different parameters:
![Function overloading mind map](/assets/img/2025-07-27-function-overloading/mind-map.png)

<span style="color: magenta">**It's important that you need add return type of functions MANDATORY.**</span> Because TS cannot define return type of function or function overload automatically.

Below is the rewritten code with the typescript and function overloading:

```typescript
// Function overloads
function combine(input1: number, input2: number): number;
function combine(input1: string, input2: string, input3?: string): string;

// Function implementation
function combine(input1: number | string, input2: number | string, input3: string = ""): number | string {
  if (typeof input1 === "number" && typeof input2 === "number") {
    return input1 + input2; // Add numbers
  } else if (typeof input1 === "string" && typeof input2 === "string") {
    return input1 + input2 + input3; // Concatenate strings
  }
}

// Using the function
console.log(combine(10, 20)); // Returns 30
console.log(combine("Hello, ", "World!")); // Returns "Hello, World!"
console.log(combine("Hello", "World", "!")); // Returns "HelloWorld!"
// console.log(combine("Hello", 10)); // Throws an error
```

When calling functions, we see that the intellisense shows us that there are two overloads and we can choose one of them:

![Function overloading example](/assets/img/2025-07-27-function-overloading/1.png)

In case you try to pass the parameters of which are not in the signature, you will get an error.

![Function overloading error example](/assets/img/2025-07-27-function-overloading/2.png)

## 3. Conclusion

This way is <span style="color: green">**suitable when**</span> you need a feature to <span style="color: green">**support two versions**</span>. 
At the moment when a new implementation is applied, but the old one is not yet deleted.
