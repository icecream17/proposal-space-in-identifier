# Space in Identifiers

## Status

This is a [stage 0](https://tc39.es/process-document/) proposal

## Motivation

There are currently many different ways to style multiple word identifiers:

```js
let flatcasename
let UPPERCASENAME
let PascalCase
let camelCase
let snake_case
let snake_Camel_Case
let Snake_Pascal_Case
```

But none of them compare to the _actual syntax_, __spaces__, used by people everywhere on the internet:

```js
let there be spaces // !!!!!!!!
```

## Benefits

<kbd>Space</kbd> is easier to press than <kbd>Shift</kbd>
```js
// Exaggerated examples

tTtTtTtTt // Hard to type
tYtYtYtYt // Hard to type
ttTttTttT // Still harder than space
t t t t t // Easy to type

// You know it's easier
node_modules
node modules

// Random line of code

```

## No way, that's impossible...!

> Most programming languages do not allow whitespace in identifiers
_- [Wikipedia](https://en.wikipedia.org/wiki/Naming_convention_(programming)#Multiple-word_identifiers)_

This seems a massive (programming language) grammar issue... but it's not!
Previously, identifiers with spaces cause a SyntaxError (unexpected identifier)
Just like how previously, BigInt numbers (`1389n`) and numeric separators (`1_000_000_003`) were SyntaxErrors.

So no code would ever have multispace variables! That's why this works!

Here's a bunch of examples
```js
"use strict";

let singleword // "singleword"
let double word // "double word" - No conflicts since previously this was a syntax error
let object.spaced property // "spaced property" - Properties also use "Identifier" (See grammar changes below)
let object. spaced property // SyntaxError (Identifier literals won't start or end in whitespace)

And i wanna know more about let tuce // Unexpected "let" (cannot contain reserved words)

// Newlines aren't part of this proposal, only spaces
singleword + double // Imaginary semicolon
word

// Identifiers still won't start or end in whitespace
let   whitespaceeeee                   // = "whitespaceeeee"

whitespaceeeee two // Previously this was a SyntaxError.
// Now it's a ReferenceError. 'Identifier "whitespaceeeee two" (which contains a space) is not defined'

// labels can also have spaces
some label: for (const char of "a string") {
    break some label;
}

function names also use Identifier(and so do parameters) {}
class Another example identifier {}

let some object = {
   some property: 32
}

do {
   let true true // Unexpected "true"
} while (false)

// This syntax can make ...interesting code
let the abc trails begin

```

## Grammar changes

```js suggestion
Identifier ::
    IdentifierName[+Strict]

IdentifierName[Strict] ::
    [~Strict] IdentifierWord
    [+Strict] IdentifierWord but not ReservedWord
    [~Strict] IdentifierWord ` ` Identifier[?Strict]
    [+Strict] IdentifierWord but not ReservedWord ` ` Identifier[?Strict]

(IdentifierWord is just the old IdentifierName)
    
```
