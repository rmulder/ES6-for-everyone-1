# ES6 For Everyone

A course for ES6. 19 modules, 66 videos, and 6.5 hours by [Wes Bos](https://github.com/wesbos)

Check out the [Course Website](https://es6.io/) for more detailed info.

Check out the [Course's Source Code](https://github.com/wesbos/es6.io)


### Module 1: New Variables -- Creation, Updating and Scoping
- `let` and `const` variables are both BLOCK scoped meaning they are scoped to the block (whatever brackets) they are in.

- Cannot redeclare a `let` variable in the same scope the way you can with `var`
- A `const` variable cannot be changed (as in "constant") but it's properties CAN be updated.

- an IIFE (Immediately-Invoked Function Expression) which is a function that runs before anything else and prevents variables leaking (e.g. `var name = "Andrew";`) is not necessary any longer since `let` and `const` are block scoped. Simply put them in brackets.
- in a for loop if you use `var i = 0` var is overwritten every time it loops so after the last iteration, if you call `i` (which has leaked out btw) then it will be equal the result of its last loop. `let` does not do this.

- Temporal dead zone = you cannot access a variable before it has been defined.  
```javascript
console.log(tank);  
const/let = tank;
```

- when to use `var/let/const`
    - use `const` by default
    - only use `let` if rebinding is needed
    - (`var` shouldn't be used)
    - [const is not about immutability where you can change the properties.](https://mathiasbynens.be/notes/es6-const)

### Module 2: Function Improvements: Arrows and Default Arguments
- 3 main benefits:
  - concise
  - Implicit Returns -- easy for one-liners
  - don't rebind the value of `this` inside another function (click handlers)
- Arrow functions are anonymous functions and so don't leave a very good stack trace. Put them in a variable.

- parentheses around the object literal so that the arrow function knows it's an object and not a a function block.

  ```javascript
  const win = winners.map((winner, i) => ({name: winner, race, place: i + 1}));
  ```

- big takeaway here is that we can use an arrow function for things inside of a normal function and it's going to inherit the value of this.
- order matters so if specific arguments are not passed it will return undefined
- if you want to skip passing a custom argument when defaults are present, pass undefined and will fall back to default

  - don't use `() =>` when:
    - need arguments object
    - need `this`

### Module 3: Template Strings
- template literals: back ticks! ` ${name} `is used to access a variable, function, run javascript within the string.
```javascript
`My dog ${name} is cute.`
```

- unordered list, use the map function to fill in words from an array. use the `join` function to make sure words don't include the commas from the array. this is useful when you want to loop over and get a list item as well.
use a ternary operator for conditional if statements with template strings  
```javascript
`${song.featuring ? ``(Featuring ${song.featuring})`` : ''}`
```
- if you have a string, you pass in the regular string that you want, and then you get all the pieces.

- using a tag template to add abbreviation tags to values. you can use reduce function. loops over each value and builds the string as it goes all.

- use tag templates to sanitize incoming html to prevent nasty js.

### Module 4: Additional String Improvements

```javascript
.startsWith(), .endsWith(), .includes(), .repeat()
```

### Module 5: Destructuring

-  expression that allows us to extract data from arrays, objects, maps and sets into their own variable. It allows us to extract properties from an object or items from an array, multiple at a time.
```javascript
 const {first, last, twitter} = person;
const { twitter:tweet, facebook: fb } = wes.links.social;
```

- array destructuring: use `[square brackets]`
```javascript
const [name, ID, website] = details;
```

- swapping variables.
```javascript
let inRing = 'Hulk Hogan';
let onSide = 'The Rock';   [inRing, onSide] = [onSide, inRing];
```

-  return multiple values as well as pick and choose the pieces that you want returned from a function.
```javascript
const { AUD, USD } = convertCurrency(100);
function tipCalc({ total = 100, tip = 0.15, tax = 0.13 } ={})
```

### Module 6: Iterables & Looping

```javascript
for ( const index of cuts){  
    console.log(cuts);
}
```

- `for of loop` should iterate over an array, however it's possible as long as they're an iterable, like a DOM collection, argument, string, map, or set.

```javascript
for (const paragraph of ps) {
    paragraph.addEventListener('click', function() {
        console.log(this.textContent);
    })
}
```

- until `Object.entries` is available use `for in` for objects.
```javascript
const apple = {color: 'Red',size: 'Medium',weight: 50,sugar: 10,};
for (const prop in apple){
    const value = apple[prop];
    console.log(value, prop);
}
```
### Module 7: An Array of Array Improvements
- `Array.from` will turn something into true array. use case: working with DOM elements. `Array.of` creates an array from every single argument you pass it.
```javascript
  const people = Array.from(document.querySelector('.people p'));
  const ages =  Array.of(12,4,23,62,34);
```

- `.find` and `.findIndex`. common use case: data comes back from an API.
```javascript
const code = 'BAAJqdslkaf';
const post = posts.find(post => post.code === code);
console.log(post);
```

- `.some()` and `.every()` will check the data in an array to check if some of the items meet what you're looking for or all of the items meet what you're looking for.
```javascript
const ages = [32, 15, 19, 12];
//any adults present?
const adultPresent = ages.some(age => age >= 18); //true
//all ages > 19, in order to drink?
const allOldEnough = ages.every(age => age >= 19); //false
```
### Module 8: ...Spread and ...Rest

-  spread will take every single item from an iterable and apply it into the new array.
