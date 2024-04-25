# Section 4: Functions & Methods

In this course section we're going to focus on functions as this is where the majority of the code you write will be.

- Parameters
- Function "length"
- Abstraction levels
- Splitting functions

Note: methods are just functions that are part of a class. So the same rules apply

## Analyzing key function parts

What makes up a function?

```javascript
function add(n1, n2) {
  return n1 + n2;
}
```

Working with the function should be easy/readable

The length of the function body matters

Calling the function should be readable:

```javascript
add(1, 2);
```

the number and order of arguments matter

## Keep the number of parameters low

The more parameters a function has, the harder it is to understand

The order of the arguments become harder to remember

And calling the function means more code to write.

### none

Calling a function with no arguments is very simple

```javascript
user.save();
```

Easy to understand

Easy to call

"Best possible option"

It will never be possible to refactor all functions/methods to have no arguments, but when you can, it's the easiest to understand.

### one

```javascript
log("message");
```

easy to understand

easy to call

no order to remember, just pass the argument

very clear what it does

very good possible option

### two

```javascript
Point(10, 20);
```

Now complexity starts to increase

Decent to understand, it's "easy" to remember that x comes first and y comes second, but order matters and has be remembered

Acceptable to call but requires some thoughts

Use with caution when you have more that 1 argument

### three

We reach the point where it's hard to justify the number of arguments

```javascript
calc(5, 10, "add");
```

Challenging to understand

Challenging to call

if we had substract, multiply, divide, it would makes us have to think/lookup the order of the arguments

Avoid if possible

### more than three

```javascript
coords(10, 3, 9, 12);
```

difficult to understand and read

difficult to call

not obvious what maps to what.

Always avoid.

## Refactoring function parameters - ideas & concepts

```javascript
function saveUser(email, password) {
  const user = {
    id: Math.random().toString(),
    email: email,
    password: password,
  };

  db.insert("users", user);
}
```

This function is not bad but when you call it, it will look like this:

```javascript
saveUser("test@test.com", "testers");
```

We probably need to dive into the function to understand what the arguments are used for.

A better approach would be to split creating the user form saving the user: 

```javascript
function saveUser(user) {
  db.insert('users', user);
}

saveUser(newUser);
```

We still have to build the user but it's clearer what the function does.

A better approach could be to use a class

```javascript
class User {
  constructor(email, password) {
    this.email = email;
    this.password = password;
    this.id = Math.random().toString();
  }

  save() {
    db.insert('users', this);
  }
}
```

Now we can call the function like this:

```javascript
const user = new User('test@test.com', 'testers');
user.save();
```

We outsourced the creation of the user to the class and the save function is now a method of the user class.

Here is a argument less function:

```javascript
let isLoggedIn = false;

function toggleLoginStatus() {
  isLoggedIn = !isLoggedIn;
}

toggleLoginStatus();
```

## When On Parameters is just right

```javascript
function log(message) {
  console.log(message);
}

log('Hi there!');
```

Wrapper around the log function only takes one, this can be useful if we want to quickly be able to swap the logging mechanism.

Other examples:

```javascript
function square(number) {
  return number * number;
}

const result = square(3);

function emailIsValid(email) {
  return email.includes('@');
}

const isValid = emailIsValid('max@test.com');

```

## Two parameters & When to Refactor

For example: 

```javascript
function login(email, password) {
  // Log a user in
  // ...
}

login('max@test.com', 'testpassword');
```

login function is a good example of a function that has two parameters. It's still easy to understand and call. The order of the arguments is expected as it's a common pattern to have email first and password second.

Another example:

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
}

const point = new Point(10, 13);
```

The order of the arguments is clear and expected.

Clean code is about minimizing the number of parameters but it's also about making sure that the parameters are easy to understand and remember.

Reducing the cognitive load of the person reading the code.

Here is a bad example:

```javascript
log('Hi there!', false);
```

Here it's obvious that we have a message, but what is false? It's not clear.

The IDE might help with the parameter names but ultimately we will probably have to look at the function definition.

```javascript
function log(message, isError) {
  if (isError) {
    console.error(message);
  } else {
    console.log(message);
  }
}
```

It is a better practice to avoid using boolean flags like this. Here we could have two separate one parameter functions:

```javascript
function logError(errorMessage) {
  console.error(errorMessage);
}

log('Hi there!');
logError('An error!');
```

## Dealing with too many parameters

What about functions that are harder to understand because they have too many parameters?

```javascript
class User {
  constructor(name, age, email) {
    this.name = name;
    this.age = age;
    this.email = email;
  }
}

const user = new User('Max', 31, 'max@test.com');
```

This code is kind of obvious what is going on but when using it, our IDE helps but it's not always clear what the parameters are (aka name first then age then email). You could argues that it should be alphabetical or that email is the most important as it should be unique and identifies the user.

Instead we could re-factor the code to use an object:

```javascript
class User {
  constructor(userData) {
    this.name = userData.name;
    this.age = userData.age;
    this.email = userData.email;
  }
}

const user = new User({ name: 'Max', email: 'max@test.com', age: 31 });
```

Now we only have 1 parameter and it's a data container that holds all the data we need that will be easier to understand and remember and validate.
Order of parameters doesn't matter anymore.

Object params is the go to solutions when you have a function that requires multiple pieces of data.

Another example:

```javascript
function compare(a, b, comparator) {
  if (comparator === 'equal') {
    return a === b;
  } else if (comparator === 'not equal') {
    return a !== b;
  } else if (comparator === 'greater') {
    return a > b;
  } else if (comparator === 'smaller') {
    return a < b;
  }
}

const isSmaller = compare(3, 5, 'smaller');
const isEqual = compare(3, 5, 'equal');
```

```javascript
function compare(comparisonData) {
  const { first, second, comparator } = comparisonData;
  if (comparator === 'equal') {
    return first === second;
  } else if (comparator === 'not equal') {
    return first !== second;
  } else if (comparator === 'greater') {
    return first > second;
  } else if (comparator === 'smaller') {
    return first < second;
  }
}

const isSmaller = compare({ first: 3, second: 5, comparator: 'smaller' });
const isSmaller = compare({ comparator: 'equal', first: 3, second: 5 });
```