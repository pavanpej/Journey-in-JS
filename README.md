# Intro to JS

>Course on [Scrimba](https://scrimba.com/g/gintrotojavascript).
>
>Some prior programming experience is needed when reading these notes to understand things like variables, data types, and some data structures like arrays and objects. 





## Numbers

- For numbers, define custom decimals using 

  - `toFixed()` - For decimals after dot
  - `toPrecision()` - For total length of number

- No definite primitive data types in JS, only type `Number`.

- Convert to number using `Number()`. Note that this converts any string to number, but that string should only contain digits inside.

- Two types of numbers are `Int` and `Float` (but are not primitive datatypes). Convert between them using `parseInt()` and `parseFloat()`.

- Note that `parseInt()` and `parseFloat()` can convert strings even if they contain non number characters.

  ```javascript
  let example1 = parseInt("33 World 22");
  let example2 = parseFloat('44 Dylan 33');
  let example3 = 55.3333.toFixed(0);
  let example4 = 200.0.toFixed(2);
  let example5 = parseInt("hello 35 hello");
  
  console.log(example1); // 33 - type Number
  console.log(example2); // 44 - type Number
  console.log(example3); // 55 - type String
  console.log(example4); // 200.00 - type String
  console.log(example5); // null - type Number
  ```



## Strings

- Check out **template strings**. They are new in **ES6** in which we do away with normal string concatenation with `+` and use back ticks (\`\`)  and `${}`to enter variables inside a string literal.
- Every string has a `.length` property (*which is not a method*).
- Some methods are `toUpperCase()`, `toLowerCase()`, `split()`, etc. Refer documentation for strings on [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String).



## Boolean

- Variables have *“truthiness”* and *“falsiness”*.

- You can use the `Boolean()` function to find out if an expression (or a variable) is 
  true or false.

  ```javascript
  Boolean(10 > 9)		// returns true
  
  // Boolean() on each of the following returns
  // the value given in the comment on the right.
  let example1 = false; 		// false
  let example2 = true; 		// true
  let example3 = null; 		// false
  let example4 = undefined; 	// false
  let example5 = ''; 			// false
  let example6 = NaN; 		// false
  let example7 = -5; 			// true
  let example8 = 0; 			// false
  ```



## Arrays

- These are lists of variables or Objects. **There can be values of different types in the same array.**

> - They have `.length` property just like strings.
>
> - Can be indexed using square braces ( `array1[<index>]` ). Indexing starts from 0.
>
> - Has methods to add and delete elements *(stack style)* like `push()` and `pop()`.
>
> - To iterate over every element of the array, use the `forEach()` method.

  ```js
  let example1 = [5, 7, 6];
  
  example1.push(8, 9, 10); 	// adds all at end
  example1.pop(); 			// removes 10
  
  example1[0] = 1; 			// changes 5 to 1
  
  // used for iterating over each element
  example1.forEach((element) => {
      console.log(element);
  });
  
  console.log(example1)
  
  // Final output looks like this:
  // 1
  // 7
  // 6
  // 8
  // 9
  // [1, 7, 6, 8, 9]
  ```

- When you’re dealing with Arrays (and Objects), we are passing by reference. So if you reference an Array variable with another Array variable, a change in one will result in a change in the other. The following example illustrates this.

  ```javascript
  let example1 = ['Dylan', 5, true];
  let example2 = example1;
  
  example2.push(11);
  
  console.log(example1); // output - ['Dylan', 5, true, 11]
  console.log(example2); // output - ['Dylan', 5, true, 11]
  ```

- In order to avoid referencing the old Array, and create your own, use the **spread operator**. More [here on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax). For example:

  ```javascript
  //same example as above, but with spread operator
  
  let example1 = ['Dylan', 5, true];
  
  // here the spread operator unpacks the old
  // array into a new one
  let example2 = [...example1];
  
  example2.push(11);
  
  console.log(example1); // output - ['Dylan', 5, true]
  console.log(example2); // output - ['Dylan', 5, true, 11]
  ```

- We can also use the `.map()` method with arrow functions to populate the new array from the old Array variable. For example:

  ```javascript
  //same example as above, but with .map()
  
  let example1 = ['Dylan', 5, true];
  
  let example2 = example1.map((element) => {
     return element; 
  });
  
  example2.push(11);
  
  console.log(example1); // output - ['Dylan', 5, true]
  console.log(example2); // output - ['Dylan', 5, true, 11]
  ```



## Objects

- Objects are enclosed in curly braces `{}` and contain `key: value` pairs, where values can further be Objects themselves.

- The objects’ values are accessed using the dot operator, where the `value` of `key` of Object `obj` is accessed as `obj.key` which returns `value`. For ex:

  ```javascript
  let example1 = {
      firstName: 'John', // here each line is a property
      lastName: 'Smith',
      address: {
          city: 'Austin',
          state: 'Texas'
      },
      age: 30
      cats: ['Milo', 'Tito', 'Achilles']
  };
  
  // access firstName property
  console.log(example1.firstName); 		// returns 'John'
  
  // we can reset object values using the dot operator too
  example1.age = 31;
  
  // nested Objects are accessed like this
  console.log(example1.address.city);		// returns 'Austin'
  ```

- The `Objects` type has some methods to access the keys and values which are respectively `.keys()` and `.values()` which can be used like this:

  ```javascript
  // returns ["firstName", "lastName", "address", "age", "cats"]
  console.log(Object.keys(example1));
  
  // returns ["Dylan", "Israel", {city: "Austin", state: "Texas"}, 31, ["Milo", "Tito", "Achilles"]]
  console.log(Object.values(example1));
  ```

- To check if a specific key exists in an Object, we use `.hasOwnProperty()` like this:

  ```javascript
  console.log(example1.hasOwnProperty('firstName'));	// returns true
  ```

- If an Object is already defined, we can create new properties directly by assignment, but it doesn’t work if the property is not already defined. Ex:

  ```javascript
  let obj = {
      firstName: 'John'
  };
  
  obj.lastName.surname = 'A.J.'; // doesn't work as lastName isn't already defined
  
  obj.lastName = 'Smith';		// works
  ```

- Like Arrays, Objects are also passed by reference, so if you want to create a copy of a a previously defined Object , we use the `.assign()` method which takes in 2 arguments:

  - what we want to assign it to, and
  - what has to be copied

  ```javascript
  let example1 = {
      firstName: 'John'
  };
  
  let example2 = Object.assign({}, example1);
  
  example2.lastName = 'Smith';
  
  console.log(example1);	// returns {firstName: 'John'}
  console.log(example2);	// returns {firstName: 'John, lastName: 'Smith'}
  ```



## Operators

- **Arithmetic** : + , - , *, /, and %.

- **Relational** : < , > , <= , >= , != , **==** (compares just the value), **===**  (compares value *and* type), !== 

  ```js
  let example1 = 5 === 5;
  let example2 = 5 == '5';
  let example3 = 6 != '6';
  let example4 = 7 !== '7';
  
  console.log(example1);		// true
  console.log(example2);		// true
  console.log(example3);		// false
  console.log(example4);		// true
  ```

- **Shorthand and Unary** : ++ , -- , += , -= , /= , *= , %=

- **Logical** : && (shorthand AND) , || (shorthand OR)



## Control Flow

> Control flow is much like in C-like languages, so not much content is included here.

### Conditionals

- **If**, **Else**, and the **Else-If ladder** are similar to other programming languages that employ braces for scoping (i.e., unlike Python).
- These are used with the operators discussed above for conditions.
- **Switch** statements are also similar to C-like languages with `break` statements for each `case`.

### Iteration

- The **for**, **while** and **do-while** loops work just like in C-like languages.
- In these, `break` and `continue` can also be used to break out of the iteration flow.



## Functions

- Functions are essentially defined like in C-like languages, but the syntax is a little different.
- They are defined with the keyword **`function`** after which the function name is given.
- Each function may or may not **`return`** a value.
- Functions can also take arguments, which can have default values specified.





# Intro to ES6+

> Course on [Scrimba](https://scrimba.com/g/gintrotoes6).
>
> Some prior programming experience is needed when reading these notes to understand things like variables, data types, and some data structures like arrays and objects. 
>
> This course includes newly introduced features in ES6, ES7 and ES8. Some additions make JS a lot easier to use.





## Template Strings

- Earlier, strings in JS were just plain old sets of chars or words enclosed in quotes, and were static.

- Now, with template literals, we can include variables inside of strings.

- **Syntax** : We use **back-ticks (``)**  to write strings.

  ```js
  let example = `This is a string`;
  ```

- Variables can be included in strings using curly braces preceded by a dollar sign - `${}`

  ```js
  let name = "John";
  let greeting = `Hello ${name}!`;
  ```

  > We can even include entire expressions inside those curly braces.

- Template strings can also be **used to write multi-line strings**.



## Destructuring

> Essentially means that it gives shorthand codes to access and reassign values.

### Destructuring Objects

Properties of objects can be accessed (and reassigned) in this shorthand as illustrated below:

```js
const personalInformation = {
    firstName: 'John',
    lastName: 'Smith',
    city: 'Austin',
    state: 'Texas',
    zipCode: 73301
};

// direct access to props
const {firstName, lastName} = personalInformation;
// or, we can even reassign prop names
const {firstName: fn, lastName: ln} = personalInformation;

console.log(`${fn} ${ln}`); // returns "John Smith"
```

### Destructuring Arrays

Like Objects above, destructuring can be done for Arrays as well, as shown:

```js
let [firstName, middleName, lastName] = ['Neo', 'The', 'One'];

console.log(firstName + lastName); // NeoOne
```



## Object Literals

> Emphasizes writing less code.

If object literals are same as function arguments, we do not need to explicitly assign them as values.

```js
function addressMaker(city, state) {
    // instead of:
    // const newAdress = {city: city, state: state};
    // write:
    const newAdress = {city, state};
    
    console.log(newAdress);
}

addressMaker('Austin', 'Texas'); // {city: 'Austin', state: 'Texas'}
```



## For of Loop

In JavaScript, there is a `for` loop that iterates over an iterable data structure (like the `for` loop of Python), using which we can directly access the iterable’s elements.

```js
let incomes = [62000, 67000, 75000];
let total = 0;

for (const income of incomes) {
    console.log(income);
    total += income;
}

console.log(total); // 204000
```

It is possible for strings also.

```js
let fullName = "Neo The One";

// prints each character of fullName on a new line 
for (const char of fullName) {
    console.log(char);
}
```

**Note: You *cannot* change the values of the element it is iterating over. It is not designed to do that.**



## Spread Operator

This operator, denoted as three dots - `...` - is used to expand (*or ‘spread’*) an Array so that it can be copied to another (instead of referencing it).

```js
let example1 = [1,2,3,4,5,6];
let example2 = [...example1];
example2.push(true);

console.log(example1);    // [1, 2, 3, 4, 5, 6]
console.log(example2);    // [1, 2, 3, 4, 5, 6, true]
```

> It can be used with Objects as well.



## Rest Operator

- Similar to the spread operator
- **Used** in functions when we **don’t know the number of arguments being passed**.

```js
// without rest operator
function add(nums) {
console.log(nums);
}
add(4, 5, 7, 8, 12) // returns 4

// with rest operator
function add(...nums) {
console.log(nums);
}
add(4, 5, 7, 8, 12) // returns [4, 5, 7, 8, 12]
```



## Arrow Functions

> Extremely useful

- Before ES6, we used to write `function () { ... }` for all callbacks. Now, we have arrow functions which makes the code a lot less bloated, and eliminates some unnecessary callback boilerplate.
- **Note:** One disadvantage is that arrow functions do not have their own instance of the `this` reference.

```js
function add(...nums) {
// here .reduce() applies the callback function
// to every element of the called Array.
let total = nums.reduce((x, y) => x + y);

console.log(total);
}

add(4, 5, 7, 8, 12) // returns 36
```



## Default Params

- These have existed in other programming languages for some time, but are introduced in JS from ES6.
- They prevent some forced error checking and ensures smoother execution.

```js
function add(numArray = []) { // empty array by default
    let total = 0;
    numArray.forEach((element) => {
        total += element;
    });
    
    console.log(total);
}

add(); // notice we don't send in an arg, but it still returns 0
```



## `includes()`

- Earlier, if we needed to check if an element is present inside an Array, we used the `.indexOf()` method. This is because it returns `-1` if the element is not present inside the Array, and then we could use that in a conditional statement.
- ES6 introduces the `.includes()` method that returns a **boolean** value of `true` if the element is present, `false` otherwise.



## `let` and `const`

- The `var` declaration was used to originally to declare variables, but the JS interpreter ‘hoists’ the variable while interpreting like this:

  ```js
  if (false) {
      var example = 5;
  }
  
  console.log(example); // null
  
  // the above works like this (hoisting occurs):
  /*
  var example;
  
  if (false) {
      example = 5;
  }
  */
  ```

- The `let` declaration prevents this hoisting, and works exactly how you write it:

  ```js
  if (false) {
      let example = 5;
  }
  
  console.log(example) // ReferenceError: example is not defined
  
  /* the above works like this (no hoisting, exactly as how it is written):
  if (false) {
      let example = 5;
  }
  */
  ```

- The `const` declaration is weird in that it doesn’t allow primitives to be changed, but if a variable is an Object or Array, we can still make changes to those variables.

  ```js
  // 1
  const example = 5;
  example = 10;     // SyntaxError: unknown: "example" is read-only
  console.log(example);
  
  // 2
  const example = [];
  example.push(5)
  console.log(example); // returns [5]
  
  // 2, with error
  const example = [];
  example = 3;
  console.log(example); // SyntaxError: unknown: "example" is read-only
  
  // 3
  const example = {};
  example.firstName = 'Dylan';
  console.log(example); // returns {firstName: "Dylan"}
  ```



## Import & Export

Allow us to follow the SOLID principles, do dependency injection, and object oriented programming, essentially helping us make our code more modular.

- Keywords used are:
  - `export` : Used to export modules from one JS file to another. More [on MDN](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export). 
  - `import` : Used to import other exported modules. More [on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import).

```js
// example.js
export const data = [1,2,3];

// index.js
import { data } from './example.js';

console.log(data);    // returns [1, 2, 3]
```



## Classes

- New keywords: `class`
- Make classes similar to how you define classes in Java and C++
- `static` methods can also be defined, which can be called directly with the class name.

```js
// animal.js
export class Animal {
    constructor(type, legs) {
        this.type = type;
        this.legs = legs;
    }
    
    // we can define getters for our class
    get metaData() {
        return `Type: ${this.type}, Legs: ${this.legs}`;
    }
    
    makeNoise(sound = 'Loud Noise') {
        console.log(sound);
    }
}

// index.js
import { Animal } from './animal.js';

let cat = new Animal('Cat', 4);

cat.legs = 3;
cat.makeNoise();      // Loud Noise
cat.makeNoise('Meow');    // Meow
console.log(cat.legs)   // 3

// using getter of class
console.log(cat.metaData) // Type: Cat, Legs: 4
```

- The `extends` keyword is used to inherit properties of another class.

```js
// animal.js
export class Cat extends Animal {
    constructor(type, legs, tail) {
        super(type, legs);
        this.tail = tail;
    }
    
    // this method overrides the parent class method
    makeNoise(sound = "meow") {
        console.log(sound);
    }
}

// index.js
import { Animal, Cat } from './animal.js'; // don't forget the Cat class too!

let cat = new Cat('Cat', 4);

cat.makeNoise();      // meow

// the following still works as properties are inherited from parent
console.log(cat.metaData);  // Type: Cat, Legs: 4
```



## Promises, Async, and Await

- **Async** stands for ‘asynchronous’. What that means is that a function can execute asynchronously from the main execution, so that it doesn’t hold up the other JS that is being processed. When a function is declared with the `async` keyword before it, it gives us access to the `await` keyword to be used inside the function.
- **Await** is used when something asynchronous is happening in the function, and we have to wait for the response of that **async**  process before proceeding further.
- A **Promise** is a way of saying that a function is going to return something (a response), and only *then* can something else be done with that response. The `.then()` method is used to process Promises.

```js
const apiUrl = 'https://fcctop100.herokuapp.com/api/fccusers/top/alltime';

function getTop100Campers() {
    fetch(apiUrl)
    .then((r) => r.json())
    .then((json) => {
        console.log(json[0])
    }).catch((error) =>{
        console.log('failed');
    });
}

getTop100Campers();
// returns:
// {
//  username: "sjames1958gm",
//  img: "https://avatars1.githubusercontent.com/u/4639625?v=4",
//  alltime: 8826,
//  recent: 104,
//  lastUpdate: "2018-04-04T09:10:12.456Z"
// }
```

- Using `async` and `await`, we can write simpler and easier to understand code for the above snippet.

```js
const apiUrl = 'https://fcctop100.herokuapp.com/api/fccusers/top/alltime';

async function getTop100Campers() {
    const response = await fetch(apiUrl);
    const json = await response.json();
    
    console.log(json[0]);
}

getTop100Campers();     // returns the same JSON as above
```

- We can create our own Promises to process something asynchronously.

```js
function resolveAfter3Seconds() {
  // here, we are creating a Promise object which is returned
  // once the inner function executes
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 3000);
  });
}

// this is the normal way, without async/await
// resolveAfter3Seconds().then((data) => {
//     console.log(data);
// });

async function getAsyncData() {
    const result = await resolveAfter3Seconds();
    console.log(result);
}

getAsyncData();     // returns "resolved" after 3s
```



## Sets

Sets are unique lists of values and, much like the sets in Python and Java, these sets do not contain any duplicate values, even if initial assignment is made using duplicates.

```js
const exampleSet = new Set([1,1,1,1,2,2,2,2]);
console.log(exampleSet);      // Set [ 1, 2 ]
console.log(exampleSet.size);   // 2
```

> Sets have more functions such as `.add()`, `.delete()`, `.has()`, and `.clear()`.

