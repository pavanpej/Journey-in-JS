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


