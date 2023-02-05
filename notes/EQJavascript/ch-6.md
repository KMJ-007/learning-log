# The Secret Life of Objects

- We are going to learn how object oriented programming is done in the js
- what is OOP first ?
- ![[images/oop.png]]
## Encapsulation:

- The core idea in object-oriented programming is to divide programs into smaller pieces and make each piece responsible for managing its own state.
- Such program pieces are modeled using objects. Their interface consists of a specific set of methods and properties. Properties that are part of the interface are called _public_. The others, which outside code should not be touching, are called _private_.
- Many languages provide a way to distinguish public and private properties and prevent outside code from accessing the private ones altogether. JavaScript, once again taking the minimalist approach, does not—not yet at least. There is work underway to add this to the language.

example:
```js
class BankAccount {
    customerName;
    accountNumber;
    //for making private class # is there
    //#balance = 0;
	balance = 0;
	
    constructor(customerName, balance = 0) {
        this.customerName = customerName;
        this.accountNumber = Date.now();
        this.balance = balance;
    }

    deposit(amount) {
        this.balance += amount;
    }

    withdraw(amount) {
        this.balance -= amount;
    }

    set balance(amount) {
        if (isNaN(amount)) {
            throw new Error('Amount is not a valid input');
        }
        this.balance = amount;
    }

    get balance() {
        return this.balance;
    }
}

class CurrentAccount extends BankAccount {
    transactionLimit = 50000;

    constructor(customerName, balance = 0) {
        super(customerName, balance);
    }

    #calculateInterest(amount) {
        console.log('Calculating interest');
    }

    takeBusinessLoan(amount) {
        // Logic
        this.#calculateInterest(amount);
        console.log('Taking business loan: ' + amount);
    }
}

const karanAccount = new CurrentAccount('Karan J', 2000);
console.log(karanAccount);
karanAccount.balance = 50000;
console.log(karanAccount);
// rakeshAccount.setBalance(400);
// rakeshAccount.balance = 5000;


```

## Methods &  Prototypes

a method is a function that is a property of an object, while a prototype is an object that serves as a blueprint for creating instances of objects.

A method is a function that is called on an object, and has access to the properties and methods of that object. For example:

```js
let obj = {
  name: 'John Doe',
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

obj.greet(); // outputs "Hello, my name is John Doe"

```

A prototype, on the other hand, is an object that is used to create other objects. It provides a template for the properties and methods that are shared among instances of the object. For example:

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};

let john = new Person('John Doe');
john.greet(); // outputs "Hello, my name is John Doe"

```

the `Person` function is used as a constructor to create instances of the `Person` object, and the `greet` method is defined on the prototype, so that all instances of the `Person` object have access to it.

- for our js world, prototype can be reffered as classes
- Constructors (all functions, in fact) automatically get a property named `prototype`, which by default holds a plain, empty object that derives from `Object.prototype`. You can overwrite it with a new object if you want. Or you can add properties to the existing object, as the example does.
```js
class Rabbit {
  constructor(type) {
    this.type = type;
  }
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
}

let killerRabbit = new Rabbit("killer");
let blackRabbit = new Rabbit("black");
```

## Overriding derived properties

default ones are overrided if you give it new, if you don't want to do that then private class or method can be used using #

```js
Rabbit.prototype.teeth = "small";
console.log(killerRabbit.teeth);
// → small
killerRabbit.teeth = "long, sharp, and bloody";
console.log(killerRabbit.teeth);
// → long, sharp, and bloody
console.log(blackRabbit.teeth);
// → small
console.log(Rabbit.prototype.teeth);
// → small
```

## Maps

- they are basically json/dictionary you can say, in value you can give any function or type of var
- This Map is data strucutre and array map is method
- there are set,get and has things to use
- Maps can use any value (including functions, objects, or any other reference type) as a key, while objects can only use strings or symbols as keys.
```js
let map = new Map();

map.set('name', 'John Doe');
map.set('age', 30);

console.log(map.get('name')); // outputs "John Doe"
console.log(map.get('age')); // outputs 30

console.log(map.has('name')); // outputs true
console.log(map.has('email')); // outputs false

map.delete('name');
console.log(map.has('name')); // outputs false

map.clear();
console.log(map.size); // outputs 0

```

## Polymorphism
- they are basically subClass abstraction in simple words
- ![[Images/Polymorphism.png]]

## Symbols
- we have new data type in the house 
- Symbols are immutable (cannot be changed) and are unique
```js
// two symbols with the same description

const value1 = Symbol('hello');
const value2 = Symbol('hello');

console.log(value1 === value2); // false
```
 you can access it using [] 
 how to use it: 
```js
let id = Symbol("id");

let person = {
    name: "Jack",

    // adding symbol as a key
    [id]: 123 // not "id": 123
};

console.log(person); //{name: "Jack", Symbol(id): 123}
console.log(person[id]); //123
```
 - Symbols are not included in for...in Loop
 ```js
 let id = Symbol("id");

let person = {
    name: "Jack",
    age: 25,
    [id]: 12
};

// using for...in
for (let key in person) {
    console.log(key);
}
//name 
//age
```

## Inheritance
- ye kisko nahi pata
- real life mai jesa hota hai wesa hi isme bhi hota hai
- baap ki dolat bete ko milti hai
- parent class ki method sub-class ko miti hai 
- iske bina Object oriented programming ka kuch point hi nahi hai
- agar bete class maise baap class ko call na karna hai to ``Super``  ka use karke kar sakte ho
```js
class Shape {
    constructor(width, height) {
        this.width = width;
        this.height = height;
    }
}

class Rectangle extends Shape {
    constructor(width, height) {
        super(width, height);
        this.type = "Rectangle";
    }
}

const myRectangle = new Rectangle(5, 10);
console.log(myRectangle.width); // 5
console.log(myRectangle.height); // 10
console.log(myRectangle.type); // "Rectangle"

```

## The instanceof operator
- kesa pata lagaye ki ye bete ki dollat ye baap ka hi hai, uska pata dna test se hota hai real life mai, par js mai `instanceof`  hai
```js
class Animal { }
class Dog extends Animal { }
class Labrador extends Dog { }

const dog = new Dog();
const labrador = new Labrador();

console.log(dog instanceof Animal); // true
console.log(dog instanceof Dog); // true
console.log(dog instanceof Labrador); // false

console.log(labrador instanceof Animal); // true
console.log(labrador instanceof Dog); // true
console.log(labrador instanceof Labrador); // true

```







Exercises khud karo na pata chale to server par post karo!

- in the exericse you will learn about new dataStructure called Set, so do them, they are imp!

Static methods:
- nazayj aulad
- static method is a method declared as part of a class and is not associated with an instance of the class. Instead, it is directly invoked using the class name.
 ```js
class MathHelper {
  static square(x) {
    return x * x;
  }
}

// calling the static method
let result = MathHelper.square(5);
console.log(result); // 25
 
```


Next chapter is like a project, in that you must read and do the thing, then only then disucss karne mai maja aayega