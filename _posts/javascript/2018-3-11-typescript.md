---
layout: post
categories: javascript
title: TypeScript-Trail
---

# Installing TypeScript

```
yran global add typescript
```

# Interfaces

```typescript
interface Person {
   firstName: string;
   lastName: string;
}

function greeter(person: Person){
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Jane" + lastName: "User" }

console.log(greeter(user))

```

# Classes

```typescript
class Student {
    fullName: string;
    constructor(
        public firstName: string,
        public middleInitial: string,
        public lastname: string
    ){
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter( person : Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = new Student("Jane", "M.", "User")

console.log(greeter(user))
```

# Basic Types

__Boolean__
```typescript
let isDone: boolean = false;
```

__Number__
```typescript
let decimal: number = 6;
```

__String__
```typescript
let color: string = "blue"
color = 'red'
```

__Array__
```typescript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

__Tuple__
```typescript
let x: [string, number]
x = ["hello", 10]
```

__Enum__
```typescirpt
enum Color {Red = 1, Green = 10, Blue}
let colorName: string = Color[10]
console.log(colorName)
//Green
```

__Any__

```typescript
let list: any[] = [1, true, "free"];
list[1] = 100;
```

__Void__

```typescript
function warnUser() : void {
    alert("This is my warning message")
}

let unusable: void = undefined
```

__Never__
```typescript
function error(message: string): never {
    throw new Error(message);
}
```


