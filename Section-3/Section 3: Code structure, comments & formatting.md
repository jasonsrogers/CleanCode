# Section 3: Code structure, comments & formatting

Now let's take a look at comments & code formatting

Code readability without writing code

Comments are (mostly) bad

Code formatting & language conventions

## Bad comments

In general, avoid comments (with some exceptions)

Most comments are mostly bad because they convey redundant information that is already present in the code.

### redundant information

````typescript

`private dbDriver: any; // the database engine to which we connect`

If we rename it to `dbEngine` the comment becomes redundant.

```typescript
if(dirver === 'sql'){
    // Connect to the SQL Driver if "driver" is set to SQL
    this.dbEngine = sqlDriver;
} else {
    // Otherwise, connect to MongoDB
    this.dbEngine = mongoDriver;
}
````

The Code itself is self-explanatory, and the comment are redundant, worse, they make it a bit harder to understand the code.

### dividers/block markers

```typescript
// ***************
// GLOBALS
// ***************
let sqlDriver: any;
let mongoDbDriver: any;

// ***************
// CLASSES
// ***************
// Acts as an adapter, connecting models to various database engines (SQL, MongoDB)
```

These are fairly obvious that we are declaring a couple of globals and then a class. The comments are redundant and add noise to the code.

If we do feel the need to add them, it could be a sign that the file is too long and should be split into smaller files.

### Misleading comments

```typescript
insertData(data: any) {
    this.dbDriver.insert(data); // updates a user
  }
```

The comment is misleading, it says "updates a user" but the code actually inserts a user.

### Commented out code

```typescript
// findMany(filter: any) {
//   this.dbDriver.find(filter);
// }
```

If we need to keep the code around, we should use version control.

## Good comments

### Legal comments

```
// (c) Maximilian Schwarzmüller / Academind GmbH
// Created in 2020
```

### Explanation of intent

Explanations which can't be replaced by good naming.

For example: regex

```javascript
// accepts [text]@[text].[text], i.e. it simply requires an "@" and a dot
const emailRegex = /\S+@\S+\.\S+/;
```

### Warning of something

```javascript
// Only works in browser environment
localStorage.setItem("user", "test@test.com");
```

This example warns that the code only works in the browser environment and not in Node.js for example.

People SHOULD know about it, but it's not obvious from the code itself. You could also argue that this is a case where you should use a feature detection instead of a comment or a try-catch block.

### TODOs notes:

```javascript
findOne(id: string) {
    // Todo: Needs to be implemented
  }
```

### Documentation comments

specially if you're writing a library or a framework, you should use documentation comments.

```javascript
/**
 * Connects to the database
 * @param {string} driver - The database engine to which we connect
 */
```

## What is "Code formatting" really about?

Code formatting is really helpful for code readability.

Code formatting improves readability and transports meaning.

There are 2 main aspects to code formatting:

- vertical formatting
  Any top to bottom form of formatting, like line breaks, space between lines, grouping of code.

- horizontal formatting
  Formatting within a line, like indentation, spacing, line width.

Formatting is important and greatly improves readability.

formatting rules differ from language to language.

Follow language-specific conventions and guidelines. (simply search for " [language] style guide")

## Vertical formatting

Could should be readable like an essay - top to bottom without too many jumps.

- Consider splitting files with multiple concepts (e.g. classes) into multiple files. There is no rule on how long things should be. But for example, keeping to 1 class per file is a good rule of thumb.

- different concepts ("areas") should be separated by spacing: functions/methods.

```javascript
const path = require('path');
const fs = require('fs');
// break betweek require areas and class area
class DiskStorage {
  constructor(storageDirectory) {
    this.storagePath = path.join(__dirname, storageDirectory);
    this.setupStorageDirectory();
  }
// break between methods
  setupStorageDirectory() {
    if (!fs.existsSync(this.storagePath)) {
      this.createStorageDirectory();
    } else {
      console.log('Directory exists already.');
    }
  }
// break between methods
...
}
```

- similar concepts ("areas") should not be separated by spacing

```javascript
const logStorage = new DiskStorage("logs");
const userStorage = new DiskStorage("users");
```

```javascript
logStorage.insertFileWithData("2020-10-1.txt", "A first demo log entry.");
logStorage.insertFileWithData("2020-10-2.txt", "A second demo log entry.");
userStorage.insertFileWithData("max.txt", "Maximilian Schwarzmüller");
userStorage.insertFileWithData("maria.txt", "Maria Jones");
```

these areas are similar in their purpose, creating variables, calling storage methods.

- Related concepts should be kept close to each other

```javascript
constructor(storageDirectory) {
    this.storagePath = path.join(__dirname, storageDirectory);
    this.setupStorageDirectory();
  }

  setupStorageDirectory() {
    if (!fs.existsSync(this.storagePath)) {
      this.createStorageDirectory();
    } else {
      console.log('Directory exists already.');
    }
  }

   createStorageDirectory() {
    fs.mkdir(this.storagePath, this.handleOperationCompletion);
  }
```

`setupStorageDirectory` is called in the constructor, so it should be close to the constructor. `createStorageDirectory` is called in `setupStorageDirectory`, so it should be close to `setupStorageDirectory`.

Note: if you have 2 methods that call a 3rd method, it's a good sign that the 3rd method should be close to the 2 methods but come after them.

```javascript
    method1() {
        this.method3();
    }

    method2() {
        this.method3();
    }

    method3() {
        // ...
    }
```

it method3 is not directly next to method1 but putting method3 before method2 would make it harder to understand method2.

Ordering of methods is also important, but that's is also dependent on the language and the framework you're using.

If you're using a language with public/private/protected methods, there might be a convention to order them in a certain way.

## Formatting: Language-specific considerations

```javascript
start();

function start() {
  console.log("start");
  next();
}

function next() {
  console.log("next");
  last();
}

function last() {
  console.log("last");
}
```

Javascript makes this kind of code possible as it hoists function declarations to the top of the file. This is a feature of the language.

This won't work in Python as we can't execute a function before it's defined.

```python
# won't work
# start()

dif start():
  print('start')
  next()

# won't work because next is called before it's defined
# start()


dif next():
  print('next')
  last()


dif last():
  print('last')

# will work
start()
```

## Horizontal formatting

Lines of code should be readable without scrolling - avoid very long sentences.

use indentation even when not technically required.

BAD

```javascript
constructor(storageDirectory) {this.storagePath = path.join(__dirname, storageDirectory);this.setupStorageDirectory();}
```

Not just line breaks, but also indentation

```javascript
constructor(storageDirectory) {
this.storagePath = path.join(__dirname, storageDirectory);
this.setupStorageDirectory();
}
```

GOOD

```javascript
constructor(storageDirectory) {
    this.storagePath = path.join(__dirname, storageDirectory);
    this.setupStorageDirectory();
  }
```

- Break long statements into multiple shorter ones

BAD
```javascript
fs.mkdir(path.join(__dirname, 'temp', '2020-10', 'images'), this.handleOperationCompletion);
```

GOOD
```javascript
const storagePath = path.join(__dirname, 'temp', '2020-10', 'images');
fs.mkdir(storagePath), this.handleOperationCompletion);
```

- use clear but not unreadably long names

```javascript
const storagePathForStoringImagesInATempFolderForOctober2020 = path.join(__dirname, 'temp', '2020-10', 'images');
```

VS

```javascript
const storagePath = path.join(__dirname, 'temp', '2020-10', 'images');
```

## Challenge

Legal comment keep

```
# (c) Maximilian Schwarzmüller / Academind GmbH
```

Remove unnecessary dividers

```python
# *********
# Imports
# *********

# *********
# Main
# *********
```

Remove redundant comments 

```python
# A class which allows us to create DiskStorage instances
```

There is a twice the same comment so we keep only the one next to the code that could fail

```python
# Warning: Directory must exist in advance
    def insert_file(self, file_name, content):
        file = open(self.get_directory_path() / file_name, 'w')
        file.write(content)
        file.close()
```

Note: fixing the code is better than adding a comment

We can keep the TODO if we really can't do it now

```python
# Todo: Add proper error handling
```

### vertical formatting

Most of the code is already well formatted vertically.

```python
log_storage = DiskStorage('logs')

log_storage.insert_file('test.txt', 'Test')
```

we could remove the space between the 2 lines

### horizontal formatting

```python
file = open(self.get_directory_path() / file_name, 'w')
```
This is not too long, yet.
It could grow over time so lets split it

```python
file = open(self.get_directory_path() / file_name, 'w')
```
becomes
```python
path = self.get_directory_path() / file_name
file = open(path, 'w')
```

