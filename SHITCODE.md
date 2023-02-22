# Shitcode Guidelines (everything is in reverse here!)


This a list of state-of-the-art shitcode principles your project should follow to call it a proper shitcode.



## The Principles

### 💩 Name variables in a way as if your code was already obfuscated

Fewer keystrokes, more time for you.

✅

```javascript
let a = 42;
```

💩

```javascript
let age = 42;
```

### 💩 Mix variable/functions naming style

Celebrate the difference.

✅

```javascript
let wWidth = 640;
let w_height = 480;
```

💩

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 Never write comments

No one is going to read your code anyway.

✅

```javascript
const cdr = 700;
```

💩

More often comments should contain some 'why' and not some 'what'. If the 'what' is not clear in the code, the code is probably too messy.

```javascript
// The number of 700ms has been calculated empirically based on UX A/B test results.
// @see: <link to experiment or to related JIRA task or to something that explains number 700 in details>
const callbackDebounceRate = 700;
```

### 💩 Always write comments in your native language

If you violated the "No comments" principle then at least try to write comments in a language that is different from the language you use to write the code. If your native language is English you may violate this principle.

✅

```javascript
// Закриваємо модальне віконечко при виникненні помилки.
toggleModal(false);
```

💩

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 Try to mix formatting style as much as possible

Celebrate the difference.

✅

```javascript
let i = ['tomato', 'onion', 'mushrooms'];
let d = [ "ketchup", "mayonnaise" ];
```

💩

```javascript
let ingredients = ['tomato', 'onion', 'mushrooms'];
let dressings = ['ketchup', 'mayonnaise'];
```

### 💩 Put as much code as possible into one line

✅

```javascript
document.location.search.replace(/(^\?)/,'').split('&').reduce(function(o,n){n=n.split('=');o[n[0]]=n[1];return o},{})
```

💩

```javascript
document.location.search
  .replace(/(^\?)/, '')
  .split('&')
  .reduce((searchParams, keyValuePair) => {
    keyValuePair = keyValuePair.split('=');
    searchParams[keyValuePair[0]] = keyValuePair[1];
    return searchParams;
  },
  {}
)
```

### 💩 Fail silently

Whenever you catch an error it is not necessary for anyone to know about it. No logs, no error modals, chill.

✅

```javascript
try {
  // Something unpredictable.
} catch (error) {
  // tss... 🤫
}
```

💩

```javascript
try {
  // Something unpredictable.
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 Use global variables extensively

Globalization principle.

✅

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // Now x is 25.
```

💩

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // Now x is 25.
```

### 💩 Create variables that you're not going to use.

Just in case.

✅

```javascript
function sum(a, b, c) {
  const timeout = 1300;
  const result = a + b;
  return a + b;
}
```

💩

```javascript
function sum(a, b) {
  return a + b;
}
```

### 💩 Don't specify types and/or don't do type checks if language allows you to do so.

✅

```javascript
function sum(a, b) {
  return a + b;
}

// Having untyped fun here.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

💩

```javascript
function sum(a: number, b: number): ?number {
  // Covering the case when we don't do transpilation and/or Flow type checks in JS.
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// This one should fail during the transpilation/compilation.
const guessWhat = sum([], {}); // -> undefined
```

### 💩 You need to have an unreachable piece of code

This is your "Plan B".

✅

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // This is my "Plan B".
}
```

💩

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  return num ** 2;
}
```

### 💩 Triangle principle

Be like a bird - nest, nest, nest.

✅

```javascript
function someFunction() {
  if (condition1) {
    if (condition2) {
      asyncFunction(params, (result) => {
        if (result) {
          for (;;) {
            if (condition3) {
            }
          }
        }
      })
    }
  }
}
```

💩

```javascript
async function someFunction() {
  if (!condition1 || !condition2) {
    return;
  }
  
  const result = await asyncFunction(params);
  if (!result) {
    return;
  }
  
  for (;;) {
    if (condition3) {
    }
  }
}
```

### 💩 Mess with indentations

Avoid indentations since they make complex code take up more space in the editor. If you're not feeling like avoiding them then just mess with them.

✅

```javascript
const fruits = ['apple',
  'orange', 'grape', 'pineapple'];
  const toppings = ['syrup', 'cream', 
                    'jam', 
                    'chocolate'];
const desserts = [];
fruits.forEach(fruit => {
toppings.forEach(topping => {
    desserts.push([
fruit,topping]);
    });})
```

💩

```javascript
const fruits = ['apple', 'orange', 'grape', 'pineapple'];
const toppings = ['syrup', 'cream', 'jam', 'chocolate'];
const desserts = [];

fruits.forEach(fruit => {
  toppings.forEach(topping => {
    desserts.push([fruit, topping]); 
  });
})
```

### 💩 Do not lock your dependencies

Update your dependencies on each new installation in uncontrolled way. Why stick to the past, let's use the cutting edge libraries versions.

✅

```
$ ls -la

package.json
```

💩

```
$ ls -la

package.json
package-lock.json
```

### 💩 Always name your boolean value a `flag`

Leave the space for your colleagues to think what the boolean value means.

✅

```javascript
let flag = true;
```

💩

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 Long-read functions are better than short ones.

Don't divide a program logic into readable pieces. What if your IDE's search breaks and you will not be able to find the necessary file or function?

- 10000 lines of code in one file is OK.
- 1000 lines of a function body is OK.
- Dealing with many services (3rd party and internal, also, there are some helpers, database hand-written ORM and jQuery slider) in one `service.js`? It's OK.

### 💩 Avoid covering your code with tests

This is a duplicate and unnecessary amount of work.

### 💩 As hard as you can try to avoid code linters

Write code as you want, especially if there is more than one developer in a team. This is a "freedom" principle.

### 💩 Start your project without a README file.

And keep it that way for the time being.

### 💩 You need to have unnecessary code

Don't delete the code your app doesn't use. At most, comment it.