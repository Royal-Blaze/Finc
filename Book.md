# The Finc Programming Language

<div align="center">

<img src="finc-logo-highres.png" alt="Finc Logo" width="400" />

</div>

### Introduction

Finc is a modern, statically typed, fast, portable, and efficient programming language. Its file extension is `.fnc`.

Finc focuses on safety, low memory usage, and performance without requiring complex code structures. It is designed to be accessible to everyone, regardless of their programming experience.

## Finc — The People's Language

Finc is known as **"The People's Language"** by its creators.

---

# Contents

1. [Comments](#chapter-1-comments)
2. [Variables](#chapter-2-variables)
3. [Access Modifiers](#chapter-3-access-modifiers)
4. [Input and Output](#chapter-4-input-and-output)
5. [Operators](#chapter-5-operators)
6. [Math in Finc](#chapter-6-math-in-finc)
7. [Naming Conventions](#chapter-7-naming-conventions)
8. [Data Types](#chapter-8-data-types)
9. [Stream.Random](#chapter-9-streamrandom)
10. [Entry Point](#chapter-10-entry-point)
11. [Functions](#chapter-11-functions)
12. [Type Casting and Shadowing](#chapter-12-type-casting-and-shadowing)

---

# Chapter 1: Comments

Comments begin with the `#` character. They are ignored by the compiler and are intended to provide explanations or additional information within the source code.

```finc
# This is a
# comment.
```

---

# Chapter 2: Variables

## 2.1 Mutable Variables

Variables can be declared using the `let` keyword or by specifying their type explicitly.

```finc
let age = 10;       # Type inference
int age = 10;       # Explicit type declaration
```

## 2.2 Constants

Constants are declared using the `const` keyword. Like mutable variables, they support both type inference and explicit type declarations.

```finc
const age = 10;       # Type inference
const int age = 10;   # Explicit type declaration
```

## 2.3 Static Variables

Static variables can be declared using the `static` keyword, with either inferred or explicitly specified types.

```finc
static age = 10;
static int age = 10;
```

---

# Chapter 3: Access Modifiers

Access modifiers control the visibility and accessibility of declarations.

| Keyword | Meaning |
|---|---|
| `pub` | Public |
| `pri` | Private |
| `pro` | Protected |

If no access modifier is specified, the default visibility is **package-private**.

Example:

```finc
let pub age = 10;
```

---

# Chapter 4: Input and Output

All input and output operations in Finc are handled through `Stream`.

## 4.1 Stream Methods

```finc
Stream.writeln(String);
Stream.write(String);
Stream.format(String);

Stream.read(String);
Stream.readln(String);

Stream.input;
Stream.output;
```

> **Note:** `Stream.input` and `Stream.output` are reserved for future use.

## 4.2 FFString — Finc Formatted String

Finc uses a special string format called **FFString (Finc Formatted String)**.

FFString allows the compiler to recognize special characters and patterns within strings:

- `[]` — Placeholder or template.
- `\n` — Newline character.
- `+` — String connector (concatenation).

Unlike most programming languages, Finc uses `+` as a connector rather than an arithmetic operator, even when both operands are integers.

For arithmetic operations, use `Math.exprs(expression)` instead.

### Example 1: String Concatenation

```finc
let age = 10;

Stream.writeln("I am " + age + " years old.");

# Output: I am 10 years old.
```

### Example 2: Named Variables in FFString

```finc
let name = "finc";

Stream.writeln("I am [name].");

# Output: I am finc.
```

### Example 3: Multiple Placeholders

Placeholders can also be used to insert multiple values into a string.

```finc
let name = "finc";
let age = 1;

Stream.writeln("I am [] and I am [] day old.", name, age);

# Output: I am finc and I am 1 day old.
```

## 4.3 Escaping in FFString

Finc uses `!$` as an escape prefix.

Place it before text that FFString would normally interpret as special. The escaped characters are then printed exactly as written.

| Write | Prints |
|---|---|
| `!$[]` | `[]` |
| `!$$` | `$` |
| `!$!` | `!` |
| `!$!$` | `!$` |
| `!$!$[]` | `!$[]` |
| `!$!$!$` | `!$!$` |

This escaping rule also applies to longer sequences.

---

# Chapter 5: Operators

Finc supports the following operators:

| Operator | Meaning |
|---|---|
| `*` | Multiplication (inside `Math.exprs` only) |
| `/` | Division (inside `Math.exprs` only) |
| `+` | Addition (inside `Math.exprs` only) |
| `-` | Subtraction (inside `Math.exprs` only) |
| `%` | Modulus (inside `Math.exprs` only) |
| `>>` | Increment |
| `<<` | Decrement |
| `=` | Assignment |
| `==` | Equality |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |
| `+=` | Add and assign |
| `-=` | Subtract and assign |
| `*=` | Multiply and assign |
| `/=` | Divide and assign |
| `!` | Logical NOT |
| `&&` | Logical AND |
| `||` | Logical OR |

### Arithmetic Restrictions

The arithmetic operators `+`, `-`, `*`, `/`, and `%` cannot be used for arithmetic outside `Math.exprs(...)`.

All other operators, including `>>`, `<<`, and compound assignment operators such as `+=`, work normally outside `Math.exprs(...)`, provided they are used for their intended purposes.

---

# Chapter 6: Math in Finc

Finc's `Math` provides all the functions available in Java's `Math` class.

To perform arithmetic operations, the entire expression must be placed inside `Math.exprs(...)`.

Expressions support nested parentheses without a predefined nesting limit.

### Examples

```finc
let number = Math.exprs((2 * 2) + 2);  # Works

let number = (2 * 2) + 2;              # Does not work
```

---

# Chapter 7: Naming Conventions

Hyphens (`-`) are not permitted in identifiers.

Finc follows the following naming conventions:

### Classes — PascalCase

```finc
FirstSecondThird
```

### Functions — camelCase

```finc
readln
getString
```

### Variables — camelCase

```finc
read
readLine
```

---

# Chapter 8: Data Types

Finc supports scalar and reference data types.

Unlike Java, Finc does not require literal suffixes such as `f` or `l` when declaring floating-point or long integer values.

### 8.1 Type Inference

Finc automatically determines the type of integer literals based on their values.

- If a whole number fits within the `int` range, it is inferred as `int`.
- If a whole number exceeds the `int` range but fits within the `long` range, it is inferred as `long`.

### 8.2 Available Data Types

| Category | Type | Size |
|---|---|---|
| Integer — Scalar | `byte` | 8-bit |
| Integer — Scalar | `short` | 16-bit |
| Integer — Scalar | `int` | 32-bit |
| Integer — Scalar | `long` | 64-bit |
| Floating Point — Scalar | `float` | 32-bit |
| Floating Point — Scalar | `double` | 64-bit |
| Boolean — Scalar | `bool` | 16-bit |
| Character — Scalar | `char` | 32-bit |
| Text — Reference | `String` | Reference |

### 8.3 Booleans

A `bool` has two possible states:

- `true`
- `false`

Use `.inInt()` to convert a boolean into an integer:

- `true` becomes `0`.
- `false` becomes `1`.

Example:

```finc
let ready = true;
let code = ready.inInt();  # 0
```

---

# Chapter 9: Stream.Random

Finc introduces `Stream.Random`, a built-in random number generator.

It can be accessed as follows:

```finc
const random = Stream.Random;
```

---

# Chapter 10: Entry Point

The `main` function is the entry point of every Finc program. It is the first function executed when a source file is run.

Finc follows these rules:

1. If a source file contains a `main` function, the program can be executed directly.
2. If a source file does not contain a `main` function, it cannot be executed independently.
3. To execute a function from a source file without a `main` function (including an entry function with a different name), call that function from the `main` function of another source file. Then execute the other file.

### Example

```finc
fn main() {
    const random = Stream.Random;

    let age = random.nextVar(incl, excl);       # With type inference
    int exactAge = random.nextInt(incl, excl);  # With explicit typing
}
```

---

# Chapter 11: Functions

Functions are declared using the `fn` keyword.

## 11.1 Function Structure

```finc
fn name() : returnType -> modifier, accessModifier {
    # The return type is specified only when explicitly declaring it.

    return {value};

    # The return type can be omitted to enable type inference
    # based on the returned value.
}
```

### 11.2 Function Rules

- Functions inherit their access modifiers from their containing classes.
- The `main()` function is always public.
- Functions are static by default.
- To declare a non-static function, use the `unstat` modifier.

### Example: Non-Static Function

```finc
fn getName() -> unstat, pub {
    return "finc";
}
```

---

# Chapter 12: Type Casting and Shadowing

Finc supports type conversions between scalar types and `String`.

## 12.1 String Conversions

| Method | Description |
|---|---|
| `toInt()` | Extracts all integer digits from the string and converts them into an integer. |
| `toByte()` | Performs the same operation as `toInt()`, returning a `byte`. |
| `toShort()` | Performs the same operation as `toInt()`, returning a `short`. |
| `toLong()` | Performs the same operation as `toInt()`, returning a `long`. |
| `toFloat()` | Extracts integer digits and converts the result into a floating-point value. |
| `toDouble()` | Performs `toInt()` and appends `.0` to the result. |
| `toChar()` | Returns the first character of the string. |
| `toBool()` | Returns `true` if the string's length is even; otherwise, returns `false`. |

Example:

```finc
let value = "ieu3ihjiu342";

let number = value.toInt();  # 3342
```

## 12.2 Integer Conversions

Applicable to `byte`, `short`, `int`, and `long`.

| Method | Description |
|---|---|
| `toString()` | Converts the number into a string representation. |
| `toDouble()` | Converts the number into a double by appending `.0`. |
| `toChar()` | Takes the first digit of the integer and converts it into a character. |
| `toBool()` | Returns `true` if the number is even; otherwise, returns `false`. |

## 12.3 Floating-Point Conversions

Applicable to `float` and `double`.

| Method | Description |
|---|---|
| `toString()` | Converts the floating-point value into a string representation. |
| `toInt()` | Removes the fractional part of the number. |
| `toChar()` | Converts the integer part into a character using its first digit. |
| `toBool()` | Converts the integer part and checks whether it is even or odd. |

## 12.4 Character Conversions

Applicable to `char`.

| Method | Description |
|---|---|
| `toString()` | Converts the character into a string representation. |
| `toInt()` | Returns the numeric value (`0–9`) for digit characters. All other characters return `0`. |
| `toDouble()` | Performs `toInt()` and appends `.0`. |
| `toBool()` | Converts the character into an integer and checks whether it is even or odd. |

## 12.5 Boolean Conversions

Applicable to `bool`.

| Method | Description |
|---|---|
| `toString()` | Converts the boolean into a string representation (`"true"` or `"false"`). |
| `toInt()` | Returns `0` for `true` and `1` for `false`. |
| `toDouble()` | Converts the result of `toInt()` into a double by appending `.0`. |
| `toChar()` | Returns `'t'` for `true` and `'f'` for `false`. |

---

## 12.6 Variable Shadowing

Finc allows variables to be redeclared with a different type through shadowing.

This means a variable can be assigned a new type without modifying its original declaration.

### Example 1: Changing the Type

```finc
let age = 10;  # Inferred as int

age : long = Math.exprs(Integer.maxValue + 1);

# age is now a long.

age = Math.exprs(Integer.maxValue + 1);

# Does not work. This results in an exception.
```

### Example 2: Type Conversion Through Shadowing

```finc
let x : float = 2039.002;

let y = x.toInt();  # y is now an int

let x : int = 1928;  # x is now an int

x.toLong();  # x is now a long
```

---

**Finc — The People's Language.**