# Section 2: Naming - assigning names to variables, functions... 

We're going to look at the first pain point: naming.

Assigning names.

- variables, constant & properties
- functions & methods
- classes & modules

Why names matter
Rules, concepts & bad names

## Why good names matter

The core principle for naming things is: 

** Names should be meaningful ** 

it should convey the purpose of the variable, function, class, module, package, etc.

BAD EXAMPLE: 

```
const us = new MainEntity();
us.process();
if(login) {

}

```

What are `us` and `login`, MainEntity? What does `process` do? What is the type of `login`?

GOOD EXAMPLE:

```
const user = new User();
user.save();
if(isLoggedIn) {

}
```

This is the same code, but it's much easier to understand. Without knowing the full context, we can understand what the code does.

Well named "things" allow readers to understand your code without going through it in details.

Examples:

```
const user = new User();
```

```
database.insert(user);
```

```
if(isLoggedIn) {

}
```

To understand the above code, we don't need to go through the full class or function definitions and all the other code.

There is more that one way to write clean code as different people have different opinions on what is clean code.

```
const admin = new Admin();
```
vs
```
const admin = new AdminUser();
```

Both are readable and meaningful, neither is wrong.

There are however naming that are definitely wrong.

## Choosing good names

We're going to look at 3 main blocks of code:

- variables, constants
`data container` that holds a value, a reference to a value, or a reference to a function or method => user nouns or short phrases with adjectives
```
const userData = {...}
const isValid = ...
```

- functions, methods
`commands or calculated values` sends data to server, check if input is valid ... => use verbs or short phrases with adjectives

```
sendData()
inputIsValid()
```

- classes
`use classes to create "things"` a user, a product, an http request body => use nouns or short phrases with nouns

```
class User {}
class RequestBody {}
```

We're going to dive deeper, look at what is the best noun/verb/adjective to use, and what are the niche cases.

## Casing conventions and programming languages

Different programming languages have different casing conventions.

There is four main ways to case code:

- snake_case: `is_valid` `send_response` e.g. in Python => use for variables functions and methods
- camelCase: `isValid` `sendResponse` e.g. in JavaScript => use for variables functions and methods
- PascalCase: `IsValid` `SendResponse` e.g. in Python, Java, JavaScript => use for classes
- kebab-case: `is-valid` `send-response` e.g. in HTML => custom HTML Elements


## Naming variables & properties

There are 3 main types of data that we can store in a variable:

- Value is an Object or Object like:
It should describe the value: `user`, `database`
Provide more details without introducing redundancy: `authenticatedUser`, `sqlDatabase`, `customer`
- Value is a Number or String
It should describe the value: `name`, `age`
Provide more details without introducing redundancy: `firstName`, `age`
- Value is a Object
It should answer a true or false question: `isValid`, `hasError`, `loggedIn`
Provide more details without introducing redundancy: `isActiveUser`, 

`isUserLoggedIn` doesn't bring anythign more than `loggedIn` as it is users that can be logged in, not products or anything else.

## Naming Variables & properties - Examples

### Example 1

#### What is stored
A user object, name, email, age

#### Bad name
`u`, `data` 
could contain anything

#### Okay names
`userData` is a bit redundant (if it was a partial dataset/almagation of data, it would be more appropriate: `{value: 'Max', 'is_valid': true}`)
`person` is too unspecific (could be author, customer, employee, etc.)

#### Good name
`user`, `customer`
User is descriptive Customer is even more specific

### Example 2

#### What is stored
User input validation result (true/false)

#### Bad name
`v`, `val`
`val`  could stand for `value` rather than `validation`
#### Okay names
`correct`, `validatedInput`
Both terms don't necessarily imply a `true` or `false` value

#### Good name
`isCorrect`, `isValid`

## Naming functions & methods - Theory

### Function perform an operation

describe the operation: `getUser`, `response.send()`

Provide more details without introducing redundancy `getUserByEmail`

`response.sendResponse()` is redundant, `response.send()` is enough


### Function computes a Boolean.

Answer a true or false question: `isValid`, `purchase.isPaid()`

Provide more details without introducing redundancy `emailIsValid`

## Naming functions & methods - Examples

### Example 1

#### What does the function do

Save user data to a database

#### Bad name

`process(...)`, 
`handle(...)`

Both are too unspecific, what is being processed or handled?

#### Okay names

`save(...)`
`storeDate(...)`

Better but we don't know what is being saved or stored

Note: if this was a method of a class, the class name would provide the context
`user.save()`

#### Good name

`saveUser(...)` `user.store(...)`

The intent is very clear - especially with the method.

### Example 2

#### What does the function do

Validate an email

#### Bad name

`process(...)` unspecific, `save(...)` misleading (this is a validation function)

#### Okay names

`validateSave(...)`

`check(...)`

Both are not 100% leaving us guessing what is being checked or validated

#### Good name

`validate(...)`

`isValid(...)`

Both makes sense - depends on what the function does exactly

## Naming Classes - Theory

Describe the Object `User`, `Product`, `Request`

Provide more details without introducing redundancy `Customer`, `Course`

Avoid redundant suffixes `DatabaseManager`

Classes are typically instantiated, instanciating a "DatabaseManager" makes no sense.

## Naming classes - Examples

### Example 1

#### What does the class represent

A user

#### Bad name

`class UEntity`
`class ObjA`

Both are too unspecific

#### Okay names

`class UserObj`
`class AppUser`

Both class names have redundant information

#### Good name

`class User`

`class Admin`

"User" is just fine - "Admin" is more specific kind of user

### Example 2

#### What does the class represent

A Database (in code)

#### Bad name

`class Data`
`class DataStorage`

Unclear or misleading (it's not a storage class but a database class)

#### Okay names

`class Dd`

Not 100% clear what it is

#### Good name

`class Database` `class SQLDatabase`

Database is good, SQLDatabase is even more specific

## Exceptions you should be aware of

Looking a the datetime python module, we can see that the class names are not descriptive at all.

`date_today = datetime.now()` is a method but is named like a property, it's not describing a command `getNow()` and it's not returning a boolean `isNow()`
 
`date_today.strftime('%Y-%m-%d')` is also a strange name, it should stand for `string from time` but it's not clear at all.

However this is built in a core python module and we can't change it. So we have to live with it but for our code over which we have control, we should always follow the coding conventions agreed upon by the team.

`DataUtil` is normally a bad name, it falls in the same pattern as `DatabaseManager`, however for classes like `DateUtil` or `DateUtility` that contain mostly static methods, then it makes sense. It mostly grouping of functions that are related to a specific topic.

` private client: any;` since it is private, it cannot be reached from outside the class, so instead we'll use getter and setter methods to access it.

`get connectedClient() {` also a getter is a method, it is named as a property, because this getter willbe used as a property.

`db.connectedClient.query(...)`

## Common Errors & Pitfalls

`userWithNameAndAge` = User('Max', 31)`

Even without knowin the class definition, it's easy to guess that this user has a name and age. This is a redundant and would lead to even more redundancy if we had to add more properties (lastName, email, etc.)

In general it's expected that a "User" will contain some user data.

We should look into the class definition if we want to learn more about the user Object.

Names should avoid describing unnecessary or redundant details.

`user = User('Max', 31)`

Variations that describe a specific state/usage can be useful:

`userLoggedIn = User('Max', 31)`

This indicates the user should be logged in and we can use it in a context where we need a logged in user.

### Avoid sland, unclear abbreviations & disinformation

#### Slang

avoid: `product.diePlease()` `user.facepalm()` 
it might be funny to you but overall it's not useful. If I'm new to the codebase/team, this means nothing to me.

do: `product.remove()` `user.sendErrorMessage()`

#### unclear abbreviations

Avoid:
`message(n)` maybe we a printing a message to the console, maybe we're sending a message to a server, maybe we're creating a message object. It's not clear.
or 
`ymdt = '20210121CET'` maybe ymdt is a date snapshot

Do:
`product.remove()` `dateWithTimezone = '20210121CET'`

#### disinformation

Avoid:
`userList = { u1: ..., u2: ...}` => it's a dictionary, not a list

`allAccounts = accounts.filter(...)` => it's not all accounts, it's a subset of accounts

Do:
`userDict = { u1: ..., u2: ...}`
`activeAccounts = accounts.filter(...)`

### Choose distinctive names

Don't:
```js
analytics.getDailyData(day)
analytics.getDayData()
analytics.getRawDailyData(day)
analytics.getParsedDailyData(day)
```
These Methods all sound very similar, it's hard to tell when you would use which method.

Do:
```js
analytics.getDailyReport(day)
analytics.getDataForToday()
analytics.getRawDailyData(day)
analytics.getParsedDailyReport(day)
```

All methods are very distinct from each other, it's easy to chose when to call which method.

Note: we still have `getRawDailyData` but now it doesn't clash with the other methods.

### Be consistent

You could write a function to load users:

`getUsers()` or `fetchUsers()` or `loadUsers()`

You can go with either of these options 

But stick with it - throughout the codebase.

If you do 

`getUsers()` in one file and `fetchProducts()` in another, it's confusing. Is there a difference between `get` and `fetch`? If so, what is it?

## Demo

We start with bad code and will improve it.

```python
from datetime import datetime


class Entity:
    def __init__(self, title, description, ymdhm):
        self.title = title
        self.description = description
        self.ymdhm = ymdhm


def output(item):
    print('Title: ' + item.title)
    print('Description: ' + item.description)
    print('Published: ' + item.ymdhm)


summary = 'Clean Code Is Great!'
desc = 'Actually, writing Clean Code can be pretty fun. You\'ll see!'
new_date = datetime.now()
publish = new_date.strftime('%Y-%m-%d %H:%M')

item = Entity(summary, desc, publish)

output(item)
```

Class `Entity` has a constructor `__init__`

def output is a function (as it's indented outside of the class) that prints the fields of an item.

Then we have fields that are used to create an `Entity` object.

What is this code doing logically?

Entity seems to be some sort of blog post.

So let's start by renaming the class to `BlogPost`

```python
class BlogPost:
```

what about the inputs to the constructor?

`title` is a good name, `description` is also good, `ymdhm` is not clear at all.

Let's change it to `date`, we can also assume it's the publication date. so let's call it `date_published`

```python
def __init__(self, title, description, date_published):
    ...
    self.date_published = date_published
```

What about the `output` function?

We are printing a blog post, so let's call it `print_blog_post`

```python
def print_blog_post(post):
    ...
```

What about the variables?

Their names are all messed up.

`summary` is passed to the `title` field, description is passed to the `description` field, `new_date` is passed to `date_published`

So let's rename them:
Note: for `new_date` we are storing the current date time, so let's call it `now` or `today`
`publish` sounds like a command but it's a formatted date, so let's call it `formatted_date`

```python
title = 'Clean Code Is Great!'
description = 'Actually, writing Clean Code can be pretty fun. You\'ll see!'
now = datetime.now()
formatted_date = now.strftime('%Y-%m-%d %H:%M')
```

Finally, we create the `BlogPost` object

```python
blog_post = BlogPost(title, description, formatted_date

print_blog_post(blog_post)
```

This is much clearer and easier to understand. ('it's not the only way to write clean code)

Further improvements:

the `print_blog_post` function, it's naming is kind of redundant, but `print_data` could be misleading, however a further improvement is to move the `print_blog_post` method to the `BlogPost` class and make it a method of the class.

```python
class BlogPost:
    ...
    def print(self):
        print('Title: ' + self.title)
        print('Description: ' + self.description)
        print('Published: ' + self.date_published)
```

Then we can call it like this:

```python
blog_post.print()
```

## your challenge

```python
class Point:
    def __init__(self, coordX, coordY):
        self.coordX = coordX
        self.coordY = coordY


class Rectangle:
    def __init__(self, starting_point, broad, high):
        self.starting_point = starting_point
        self.broad = broad
        self.high = high

    def area(self):
        return self.broad * self.high

    def end_points(self):
        top_right = self.starting_point.coordX + self.broad
        bottom_left = self.starting_point.coordY + self.high
        print('Starting Point (X)): ' + str(self.starting_point.coordX))
        print('Starting Point (Y)): ' + str(self.starting_point.coordY))
        print('End Point X-Axis (Top Right): ' + str(top_right))
        print('End Point Y-Axis (Bottom Left): ' + str(bottom_left))


def build_stuff():
    main_point = Point(50, 100)
    rect = Rectangle(main_point, 90, 10)

    return rect


my_rect = build_stuff()

print(my_rect.area())
my_rect.end_points()
```

`class Point:`
`class Rectangle:`

Those are good names, we could be more specific with `Point` but it's not necessary.

```python
def __init__(self, coordX, coordY):
    self.coordX = coordX
    self.coordY = coordY
```

`coordX` and `coordY` are ok and could be left as is, but they are not great as they are a bit redundant.

In the context of point, `x` and `y` are enough as it's clear that they are coordinates.

So in this case, shorter names are better.

```python
 def __init__(self, starting_point, broad, high):
    self.starting_point = starting_point
    self.broad = broad
    self.high = high
```

The constructor of the `Rectangle`, the variable names are not great.

`starting_point` is ok, it's coordinates where to start the rectangle, a possible improvement could be `origin`

`broad` and `high` are not good, they are slang and unclear when there is more common words to describe a rectangle's dimensions: `width` and `height`

```python
def area(self):
    return self.broad * self.high
```

Is a method and therefore should have a name that describes an action performed by the method. This sounds like a property, which would be fine if a boolean was returned or if it was a getter. Instead let's call it `get_area`

```python
def end_points(self):
    top_right = self.starting_point.coordX + self.broad
    bottom_left = self.starting_point.coordY + self.high
    print('Starting Point (X)): ' + str(self.starting_point.coordX))
    print('Starting Point (Y)): ' + str(self.starting_point.coordY))
    print('End Point X-Axis (Top Right): ' + str(top_right))
    print('End Point Y-Axis (Bottom Left): ' + str(bottom_left))
```

This is printing the end points of the rectangle. 
The variables `top_right` and `bottom_left` are good enough, we could find alternatives but they are clear enough.

`end_points` we are not just printing the end points, we are also printing the starting point, so let's call it `print_coordinates`

```python
def build_stuff():
    main_point = Point(50, 100)
    rect = Rectangle(main_point, 90, 10)

    return rect
```

This is slang and unclear, `build_stuff` is not descriptive at all and we have to look into the function to understand what it does.

`build_rectangle` would be a better name.

`main_point` is not a good name, it's the origin of the rectangle, so let's call it `rectangle_origin`

`rect` is an unclear abbreviation, `rectangle` is better.

```python
my_rect = build_stuff()

print(my_rect.area())
my_rect.end_points()
```

`my_rect` is just bad, `my` is it the developers rectangle? the users? the applications? It's unclear.

`rectangle` is better.