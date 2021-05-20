# Space in Identifier

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

Too many

What's also _too many_ is the _milliseconds_ taken pressing the shift key:

<!--  \lol (not \s) -->
```js
tryTypingThis(ughShiftWhy)

now type this(much easier)
```

But why not use the actual syntax, _spaces_, used by people everywhere on the internet:

```js
let ters and spaces
```

```js
let tersAndSpaces
```
## Solution

Now, as you may know,

> Most programming languages do not allow whitespace in identifiers
_- [Wikipedia](https://en.wikipedia.org/wiki/Naming_convention_(programming)#Multiple-word_identifiers)_

And, isn't this a massive grammar issue?
It isn't! Previously this was a SyntaxError (unexpected identifier), so actually there's no conflicts!

```js
let singleword // "singleword"
let double word // "double word" - No conflicts since previously this was a syntax error
let object.spaced property // "spaced property" - Same thing
let object. spaced property // SyntaxError (Identifier literals won't start or end in whitespace)

And i wanna know more about let tuce // Unexpected "let" (cannot contain reserved words)

// Newlines aren't part of this proposal, only spaces
singleword + double // Imaginary semicolon
word

// Identifiers still won't start or end in whitespace
let   whitespaceeeee                   // = "whitespaceeeee"

whitespaceeeee singleword // Still Error. But previously this was a syntax error.
// Now it's a ReferenceError. "Identifier containing whitespace (%s) is not defined"

// labels can also have spaces
some label: for async (const char of "a string") {
    break some label;
}

function names are also identifiers(and so are parameters) {}
class Another example with spaces {}

let some object = {
   some property: 32
}

do {
   let true true // Unexpected "true"
} while (false)

// This syntax can make code not look like code
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
