# Section 1: Getting started

What is clean code and why is it important?

## What is clean code?

Side Note: functions that create functions are `factory functions` or `higher order functions`

```python
max = create ('Max', 31)
```

It looks like the function is creating a user `Max` with age `31`. But if we look at the full code: 

```python
def create(m, n):
    if m == 'Max':
        return lambda v: v < n
    else: m == 'Min':
        return lambda v: v > n

max = create('Max', 31)
```

Now we can see it's a function that returns a Max function.

This is not clean code as the code is confusing and hard to understand without the full context.

Clean code, it's not about whether code works.

As a developer, a vast majority of time is spent reading and understanding code. We need to read code and understand it. So it's important to write code that is easy to read and understand

Here's a way to write this code in a cleaner way:

```python
def create_validator(mode, number):
    if mode == 'Max':
        return lambda value: value < number
    else: mode == 'Min':
        return lambda value: value > number

is_below_max = create_validator('Max', 31)
```

Just by changing the name of the function and the variable, the code is much easier to understand.

There are other ways to write this code in a clean way, and there never will be a single way to write clean code. But the important thing is to write code that is easy to read and understand, following a common style and convention.

So what is clean code?

- should be readable and meaningful
- should reduce cognitive load
- should be concise and "to the point"
- should avoid unintuitive names, complex nesting and big code blocks
- should follow common best practices and patterns
- should be fun to write and to maintain

Clean code is easy to understand, dirty code is note

Write a good story: 
- your code is like an essay
- you are the author
- write it such that it's fun and easy to read and understand

## Clean Codde - Key pain points  & How to write clean code

There are various pain points in writing clean code. We are going to look into the following pain points and how to write clean code:

- Names: variable, function, class, module, package
- Structure and comments: code formatting, good and bad comments
- Functions: function length, function arguments
- Conditionals and error handling: Deep nesting, missing error handling
- Classes & Data structures: missing distinction, bloated classes

What a are the solutions to these pain points?
- rules & concepts
- patterns & principles
- test driven development

## Course prerequisites

- programming experience is required
- We're mostly going to use Python and JavaScript/TypeScript (but the concepts are applicable to any language)

## Clean code & strongly typed languages

Clean code doesn't require strong typing

```ts
function add(num1: number, num2: number) {
    return num1 + num2;
}
```

Here the types don't add much value. 

Types can help preventing errors and can improve readability. It performs an extra layer of validation.

But code can also be 100% readable and meaningful without types.

```js
function add(num1, num2) {
    return num1 + num2;
}
```

## About the course code examples

Examples are short, focused examples focused around a particular concept.

Code snippets: Most won't execute as they are out of concept

Example don't use a particular style / paradigm

## Join Our Learning Community!
Great to have you on board as a student!

This course also comes with free access to our “Academind Community” on Discord: https://academind.com/community/

---

There, you can find like-minded people, discuss issues, help each other, share progress, successes and ideas and simply have a good time!

I believe that you learn the most if you don’t learn alone but find learning partners and other people with similar interests. Our community is a great place for this - it’s the perfect complimentary resource for this course.

Joining it is of course free and 100% optional! :-)

We'd love to welcome you on board of the community!

## Functional, OOP, Procedural: the course concepts always apply

This course doesn't focus on a specific praradigm

Paradigm-specific rules, conventions, patterns and guides should also be considered

The core principles & rules always apply

No matter which programming language or style you're using...

- you still want readable and meaningful names
- you still want slim, concise functions or methods
- you still want understandable code flow

## Clean code, principles & patterns & clean architecture

clean code => is code which is readable and easy to understand

pattern & principles => write code which is maintainable and extensible

The two are not exclusive, they are complementary

Clean code Vs Clean architecture

Clean code:
- how to write the code
- focus on single problems/files

Clean architecture:
- where to write which code
- how to structure the code
- focus on the project as a whole

## Clean code vs quick code

Writing clean code takes time

Of course you want to write your best code right from the beginning

You will always finds ways of improving your code

As your project evolves, your code will need changes 

=> question old code and refactor it

Writing clean code is an iterative process that is never done, as we maintain and evolve our code we'll find new ways to improve it

Embrace refactoring!

It's an intrinsic part of writing clean code and code life cycle

- refactoring today is work you save tomorrow
- a codebase can only survive and stay maintainable if it's continuously improved and refactored
- whenever you add something new, try to improve existing code along the way

We're always under pressure to deliver fast which leads to the temptation to write quick code

Overtime, quick code becomes dirty code, initially it's easy to write and output is fast, but it's hard to maintain and understand








