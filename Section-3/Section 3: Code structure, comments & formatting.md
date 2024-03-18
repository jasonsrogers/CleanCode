# Section 3: Code structure, comments & formatting

Now let's take a look at comments & code formatting

Code readability without writing code

Comments are (mostly) bad

Code formatting & language conventions

## Bad comments

In general, avoid comments (with some exceptions)

Most comments are mostly bad because they convey redundant information that is already present in the code.

### redundant information

```typescript

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
```

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
localStorage.setItem('user', 'test@test.com');
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