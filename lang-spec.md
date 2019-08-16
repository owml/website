---
layout: page
title: Language Specification
permalink: /docs/lang-spec/
---
Welcome to the language specification for Owen's Markup Language! This document will go over the formal standards of owml, alongside a quick writing tutorial.

*As you may have noticed, we use the abbriviation of `owml` for Owen's Markup Language and will continue to do so throughout this document for brevity sake.*

## Writing Owen's Markup Language

*Coming soon!*

## Owen's Markup Language Specification

### Notes

- Highlighting uses C as there is (currently) no widespread syntax highlighting built into markdown parsers that utilizes owml.
- If you are writing a parser, please stick to these standards as close as possible. They are written in an easy-to-read fashion but are **standards**, not guidelines.

### General Syntax

*Apologies about the incomplete style of the following info, there isn't a much more human-readable way of convaying this infomation.*

`[x]` means that there is a smaller definition for `x` and it will be in the bullet-points further along. `[x="y"]` Means that "x" should be reffered to as "y" in this circumstance. `[x|y|z]` means that it will pick the first method it finds to be correct. `[..]` means that this info will be extracted.

- Keypair: `[key_name="name"]: [key="data"];`
  - Key Name: `[key_string|key_int]`
    - Key: `[key_string|key_int|key_array|key_object]`
      - Key String: `"[..]"`
      - Key Int: `[..]`
- Array: `\[[key_array="item"]\]`
  - Key array: `[key];`
    - Key: `[key_string|key_int]`
      - Key String: `"[..]"`
      - Key Int: `[..]`
- Object: `{[keypair]}`
  - Keypair: `[key_name="name"]: [key="data"];`
    - Key Name: `[key_string|key_int]`
      - Key: `[key_string|key_int|key_array|key_object]`
        - Key String: `"[..]"`
        - Key Int: `[..]`

Here is a more padded-out example of this in action:

```c
"Woo": [
    123;
    23434;
    234234;
];
"Other": {
    54534: {
        "Meep": "morp";
    };
    "This is cool": [
        "yes";
        "it";
        "is";
    ];
    45345: 34535;
};
```

### Types

- String: A string type. This can be written as `'Hello'` or `"Hello"` (please include both quotation types when writing a parser).
- Int: A 32-bit signed integer that can be written as `32564` for positive numbers or `-476343` for negatives.
- Array: A strict type that infers it's type from the first used, wrapped in `[]`. If an array looked like `[ 'Hello'; 1234; ]` it would not parse due to this. **Cannot be a name inside of a keypair**
- Object: A way to split items into different nested sections. Wrapped in `{}`, it can function the same as a standard block. **Cannot be a name inside of a keypair**

#### Type Examples

**String**:

```c
"This is a string": "Hello";
'Can also use quotes': 'Yes';
```

**Int**:

```c
"The following data contains an int": 656435;
923857: "Names can be ints";
"Negative int coming up!": -158403;
```

**Array**:

```c
"This is an array": [
    "It infers";
    "The types";
    "And doesn\'t";
    "Allow 2 types";
];
"Array of arrays!": [
    [ "Hello"; ];
    [ 432434; 23; 26; 245; 3234 ];
];
```

**Object**:

```c
"This is an object": {
    "It allows": "different sections";
    6345234: {
        "erjhgejh": 4345;
        "3453fdgdfg": [
            53453;
            3522;
            3425;
        ];
    };
};
```
