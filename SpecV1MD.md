# The ECY Programming Language - Specification

# I Beginning

In modern times, the range of programming languages found in working environments has ever so slightly been decreasing over the past decades. Not a while ago, a C-Programmer would have found a job just as easy as a Java-Programmer, or any other programmer that is familiar with one of the “big languages”. But now, being a fresh C-Programmer makes life harder, not only because nobody wants an inexperienced worker over a worker with experience, but also because most jobs these days are asking for “Experienced in Python”, “Excel Strengths” and most of them all, “Vibe coding experts”, like I choose to call them.

The problem might not be instantly clear for someone who has never really coded before in their life, but let me tell you: These “modern” languages, that mostly have been designed not recent enough to be in current modern times, have big flaws. Mainly:

* Everything being dumbed down to a max

If your programming language bans brackets for being too “complicated”, I wonder how it hasn't banned classes already, because those are relatively kinda hard

* Everything deemed “too hard” deemed “unneccessary”, followed by removal

Modern languages often just remove anything that is too hard, instead of trying to find a good workaround. One example being C# dealing with pointers: They are locked behind unsafe \{} instead of being revised and made memory-safe. Wouldn't be that bad if C# tried to do that, but they only scraped the surface of possibilities. While pointers are indeed garbage collected, they could've been so much more.

* Everything is made less free to make things simple

Often times, features that exist to allow more freedom for programmers are just forgotten about, left to rot with C and C++, instead of being kept in. For languages like Python, this is explained by the heavy interpretation of the language, making extras cost a lot of performance just to be implemented, not just used. But things like C++ bit manipulation, that is completely optional, is just not included for “simplicity”. After all, if your language is not designed to be Scratch 2, bit manipulation can easily be kept in because things like that are just giving more freedom to coders. Now, I understand that a more modern language like Java is trying to be easy to learn, but something most white papers underestimate is the power of sectionizing everything. This means that this paper will always have a feature findable by the chapter and sub-chapter names.



ECY was born from that dilemma with programming languages and also another balancing issue that shouldn't even exist in the first place given good design choices, like requiring the coder to instruct the compiler to do assumptions and such using keywords or syntax structures.

# II ECY's role in the dilemma

ECY is not trying to be C# on drugs or Java with overloading, it's trying to be a solution to a problem I found in programming languages I personally use, like C++, C# and Java itself. The problem, as I see it, is the fact that for some reason, simplicity and features seem to be connected. If one goes up, the other goes down.

Take C++, for example. In C++, you can do almost anything you'd dream of: Manipulate bits, access a variable from anywhere using pointers, write an entire video game engine. But then you try to do any of these and are suddenly met with code that looks like what I'd find next to the definition of “Spaghetti Code” in the dictionary. It's not very simple to use C++. Even the “Hello, World!” program is connected with so many C++ features that trying to learn why we have to do `cout << "Hello, World!"` instead of having a designated `print()` function takes atleast 2 months of reading handbooks and scowering StackOverflow. But this is what allows you to do way too many cool things, like write a custom output stream and then writing it to the cout-stream or taking the first 5 chars of input from the cin-stream - you just can't do that in a language like Java or C#.



This is why ECY was made to be the first language to try and bring both simplicity and a rich feature set. In fact, the ECY “Hello, World!” program, or as a file you could call it “helloworld.ecy”, is one of the more simple “Hello, World!” programs:

```
println("Hello, World!");
```

No classes, no main(), no imports: ECY truly tries to keep it simple and fresh in the world of programming. But this is not the only thing the language shines at.

For example, we could look at a simple ECY struct for a complex number, which at the current time would seem rather cryptic (as usual for a new language) but the structure is exactly equal to the structs from other programming languages:

```
import <emath>; // ECY Math

public struct Complex {
  public real: f32; // A float that always is and always will be 32 bits
  public img: f32;
        
  return { mag: f32 = sqrt(real**2 + img**2); } => mag; // The magic cocaine of ECY
}
```

The entirety of ECY and its ideas can be condensed down into a single principle: _simple complexity_. _simple complexity_ is a term coined by me for how ECY is made: simple but feature-rich.

The second most important principle ECY runs on is the principle of _opting-in_. Almost any compiler & syntax sugar in the language is only useable via keywords or settings, which enables newbies to have a helping hand and veterans to know exactly how their code will run and be the most efficient at debugging.

# III How this paper will be written

So far, this paper has been written in the first person, but to follow a more straightforward way of explaining my life-long programming dream, the entirety of the explanation part of this paper will be written not in first person, not in third person, but in no person at all. It will be just raw information, no comparing with other languages, no praising itslelf in its own paper.

This is because I believe a good programming language isn't defined by its presentation but rather by its features, so wether this paper presents ECY in a good or bad light isn't answered by yes or no, but by the follow-up question “Is it objective?”. I've read through some language white papers just to read “Another great thing about…” or “This is why … is so much better than …” or even “Here is some problem from another language, and … is the solution” every few lines, making it seem like a scammy mergant trying to sell you shady things in a dark corridor by doing even shadier marketing for himself. This is why after this chapter, the entire remainder of the ECY language white paper will be written as objectively and impersonal as possible to try and get an impression, not assign one.

As I like to call it, this paper does “Teaching instead of Preaching”.

# 1 Introduction

## 1.1 Printing

### 1.1.1 The print function

Following modern principles, ECY uses a simple to write syntax for outputting values to the console:

```
print("Hello, World");
```

This print function comes in two flavors: `print()` and `println()`. `print()` prints a given literal or variable to the console while `println()` adds a line break after printing.

### 1.1.2 Limitations of the print function

The print function has a limitation for custom Objects to be printed as ECY does not have an automatically called objToString() function, but ECY contains the built-in function called `obj2str(obj: Object)` which allows you to invoke the conversion of Objects into Strings manually.

## 1.2 Inputting

### 1.2.1 The input function

Unlike most modern programming languages, ECY takes a different looking approach to inputting. There are two ways to get an input in ECY from the console, those being:

```
getInput(into: str);
getInputTo(into: str, stopChar: chr);
```

`getInput()` and `getInputTo()` both read input until a stop char and set a given string `into` to the read input. `getInput()` has the stop char set to a line break while `getInputTo()` allows customization. As of ECY-1.0, `getInput()` has no overload for stopChar implemented, so `getInputTo()` will remain the only way of achieving a `getInput()` with stopChar.

## 1.3 Variables

### 1.3.1 Declaration

In ECY, variables are declared name-first. Name-first means that the name comes before the type in declaration:

```
NAME: TYPE = VALUE;
```

Also, as visible, ECY uses the semicolon as a command end marker.

### 1.3.2 Reinitialization

Reinitialization follows the same basic principle as declaration, that being using the following syntax:

```
NAME: TYPE = VALUE;
NAME = NEWVALUE; // Reinitialization
```

### 1.3.3 Types

Types are named following a repetitive order of initial + bit width. This means that all the basic types you know are the following in ECY:

```
i8 // byte
i16 // short
i32 // int
i64 // long
i128 // long long
u8 // unsigned byte
u16 // unsigned short
u32 // unsigned int
u64 // unsigned long
u128 // unsigned long long
b1 // boolean
b32 // 32-bit boolean
b64 // 64-bit boolean
f32 // float
f64 // double
d32 // decimal
d64 // 64-bit decimal
str // string
c8 // ASCII char
c16 // Unicode char
c32 // 32-bit char
```

All these types also have a shorthand:

```
int => i32
uint => u32
bool => b1
float => f32
dbl => f64
dec => d32
chr => c8
```

There are also some postfixes for numbers:

* float postfix is -f ⇒ `var: f32 = 10.5f`
* double postfix is -d, even though ECY defaults any number to `f64` even without a -d postfix
* binary postfix is -b and binary is only useable as literals in ECY
* hex prefix is 0x

### 1.3.4 Type Conversion

Converting types in ECY is easy and automatic. Type casting is performed through the parantheses syntax:

```
num: i32 = 15;
var: f32 = 52.6f;
num = (i32)var;
```

Even though, in cases like above, ECY can even automatically detect a conversion and perform auto-casting, which still has to be enabled manually for every project to avoid forced assumption by the compiler.

While it should be enabled by default (and this is assumed in the entire whitepaper's code), you can disable it either by setting the compiler optimization level to 0 (see “9.0 Compile-Time Code Handling”) or by enabling it globally in the project settings.

### 1.3.5 Placeholder variables

ECY enables the usage of the `_` placeholder, a special variable avaiable in any ECY project. The placeholder variable is actually not a variable and instead instructs the compiler to create a register value with the given input. Here is an example allowing you to print a non-existent variable:

```
println(_: i32 = 5);
```

This placeholder is useful as it can also create ghost instances of classes. ECY even resolves any ephemeral allocation caused by the placeholder variable automatically as it's part of the language itself.

The `_` placeholder also stays on its register until overridden by either a literal or an assignment to the placeholder itself. For any type or object whose `sizeOf(type)` is too big for fitting in less than 4 registers, a reference to the given data is used. In the case of a literal, new memory is allocated either on the stack or the heap, depending on what is actually placed into the placeholder.

### 1.3.6 String conversion

Strings can now automatically convert any value into a string thanks to the automatic type conversion behavior by ECY, which is enabled by default only for strings and chars. Here is an example of converting a float to a string and printing it out:

```
val: f32 = 21.01f;
txt: str = val;
println(txt); // prints 21.01
```

You can also make usage of the `obj2str` function or even the `num2str` function, which includes an overload for enabling and disabling the float marker and has support for localization via another overload:

```
num2str(in: Object);
num2str(in: Object, localize: bool);
num2str(in: Object, localize: bool, marker: bool);
```

That way you can use `num2str` when converting a number into a string as in above example:

```
val: f32 = 21.01f;
txt: str = num2str(val, false, true);
println(txt); // now prints 21.01f
```

### 1.3.7 String Parsing

ECY is equipped with a built-in parse function from string to every primitive data type. Each of those functions is named parseToTYPE, where TYPE is replaced by the given parsing type. Here is an example of parsing a string to i32:

```
num: i32;
txt: str = "25";
num = parseToi32(txt);
```

You can also use the more sophisticated `parseTo()` function, which includes the ability to specify the primitive data type in question:

```
parseTo(in: str, t: freestr);
```

### 1.3.8 Freed Strings

Freed strings are a brand new concept avaible in ECY that allows for the use of strings as parameters without requiring double quotes, even though double quotes can still be used.

Freed strings can only be used in function parameters and to create one you use the `freestr` type. Here is an example usage with `parseTo()`:

```
// parseTo(in: str, t: freestr)
parseTo("Hello, World", i32); // => parseTo("Hello, World", "i32");
```

Freed strings are special in that they are the only string type to end on these symbols:

* ,
* )
* whitespace

Freed strings also take precedence in the parser over keywords, but since they only exist inside parameter lists, no extra parsing and linking has to be done unless inside a parameter list.

### 1.3.9 SAIF (Shorthand Auto-Initialization Feature)

SAIFs are a new concept in ECY that allows for variables to be declared in a fast and quick way. The syntax for a SAIF looks like the following:

```
NAME.SHORTHAND{VALUE};
```

SAIF Shorthands are short versions of type names used in SAIFs only. For every type, these are the respective SAIF Shorthands:

```
i8 => byte
i16 => short
i32 => int
i64 => long
i128 => xlong
u8 => ubyte
u16 => ushort
u32 => uint
u64 => ulong
u128 => uxlong
f32 => fl
f64 => dbl
b1 => bool
b32 => b32
b64 => b64
d32 => dec
d64 => lec
str => str
c8 => chr
c16 => wchr
c32 => xwchr
```

SAIF can only be used to declare new variables, and not to assign existing ones. Here is an example of using SAIF efficiently:

```
num.int{0};
txt.str{""};
getInput(txt);
num = parseTo(txt, i32);
println(num);
getInput(txt);
val.int{parseTo(txt, i32)};
println(val);
```

As visible, the initialization value of a SAIF can also be any term or function call that returns a value of the given type.

### 1.3.10 SAF (Shorthand Assignment Feature)

SAF is yet another shorthand syntax for variables, but used for assigning existing variables. The syntax for SAF is defined as:

```
NAME(NEWVALUE);
```

It's recommended that SAFs are only used for assignment functions and quick assignment to avoid a loss of readability from overusing SAFs, and the compiler will recommend the usage of a normal assigning when an SAF is used outside the above described context, but will not force the replacement.

Like SAIF, the assigning value of a SAF can be any term or function call that returns a value of the correct type.

### 1.3.11 What obj2str does

`obj2str` is actually an internal structural function that gets inlined around the converted object during runtime or, in the case of a primitive, sent to a special `prim2str` function.

The output of `obj2str` is as following:

```plaintext
[field1name: field1value, field2name: field2value, field3name: field3value, ...]
```

### 1.3.12 \$-string literals

To allow for the faster creation of string-variable constructions, ECY uses the \$-string literal. This kind of string allows for the injection of variables into itself via `{VAR}`, which is replaced by a value appension during compile-time:

```
a: i32 = 42;
println($"a = {a}"); // Prints "a = 42"
```

\$-string literals cannot contain literal values inside `{}`, but they can contain any term that results in a single value and contains variables.

### 1.3.13 Built-In object functions

* `typeOf(obj: Object)`: Returns the type of the object.
* `sizeOf(obj: Object)` or `sizeOf(definition)`: Returns the size of the given type (/definition) or object.
* `nameOf(obj: Object)`: Returns the name of the object. For \$-string literals, `#` can be used instead like `#x`
* `familyOf(type)`: Returns the family of the type.

# 2 Operators

## 2.1 Basic Operators

### 2.1.1 Operator Types

ECY has three main types of value operators, those being:

* Assignment Operators (AsO)
* Arithmetic Operators (ArO)
* Comparison Operators (CO)
* Bitwise Operators (BO)
* Logical Operators (LO)

### 2.1.2 Assignment operators

There are different assignment operators (AsO) in ECY. The main assignment operator is the equality sign `=`, used to set values of objects:

```
var: i32;
var = 25;
num: i32 = 20;
var = num;
```

Before we get to further AsOs, we'll have to get to ArOs.

### 2.1.3 Arithmetic operators

Arithmetic operators allow for the arithmetic transformation of values. There are six base arithmetic operators in ECY:

* Addition Operator

The addition operator uses the plus symbol `+` and returns the sum of the left- and the righthand value. ECY also performs automatic conversion for numerical values.

```
5 + 5
=> 10
5 + 6
=> 11
7.4f + 2.5f
=> 9.9f
1.3f + 2
=> 3.3f
9 + 9d
=> 18.0d
2.4f + 2.4d
=> 4.8d
```

* Subtraction Operator

The subtraction operator uses the minus symbol `-` and returns the difference of the left- and the righthand value. ECY also performs automatic conversion for numerical values.

```
5 - 5
=> 0
5 - 6
=> -1
7.4f - 2.5f
=> 4.9f
1.3f - 2
=> 0.7f
9 - 9d
=> 0.0d
2.4f - 2.4d
=> 0.0d
```

* Multiplication Operator

The multiplication operator uses the star symbol `*` and returns the product of the left- and the righthand value. ECY also performs automatic conversion for numerical values.

```
5 * 5
=> 25
5 * 6
=> 30
7.4f * 2.5f
=> 18.5f
9 * 9d
=> 81.0d
```

* Division Operator

The division operator uses the slash symbol `/` and returns the division of the left- and the righthand value. ECY also performs automatic conversion for numerical values.

```
5 / 5
=> 1
10 / 2
=> 5
7.5f / 2.5f
=> 3
9 / 9d
=> 1.0d
9f / 9d
=> 1.0d
9 / 9f
=> 1.0f
```

* Modulo Operator

The modulo operator uses the percent sign `%` and returns the remainder of the division of the left- and the righthand value. ECY also performs automatic conversion for numerical values.

```
5 % 5
=> 0
5 % 6
=> 5
9d % 2.5f
=> 1.5d
9 % 9d
=> 0.0d
```

* Exponentiation operator

The exponentiation operator uses a double star `**` as its symbol and returns the lefthand value to the power of the righthand value. ECY performs automatic conversion for numerical values.

```
5 ** 2
=> 25
10 ** 4
=> 10000
3 ** 3
=> 27
4 ** 0.5f
=> 2.0f
4 ** 0.5d
=> 2.0d
4d ** 0.5f
=> 2.0d
```

### 2.1.4 Condensed arithmetic operators

ECY allows for arithmetic operators to be condensed and combined with the assignment operator. This condensed arithmetic operator will act like assigning a variable with the arithmetic operation applied to the variable itself:

```
var = var ? VALUE;
```

Where `?` is any arithmetic operator, `var` is any variable and `VALUE` is any value that can be combined with `var` arithmetically.

Condensing a construction like above results in this term:

```
var = var ? VALUE;
// Condenses to:
var ?= VALUE;
```

It is important to know that this condensed operator will always result in the same expanded term structure:

```
var: i32 = 15;
num: i32 = 23;
var += num;
// Always equal to:
var = var + num;
```

Only one `var ? VALUE` term can be condensed at once and any extra term may either be kept as is or has to be calculated seperately:

```
var = var + num * 10;
// Condenses to:
var += num * 10;

var = var * 10 + num - 5;
// Condenses to:
var *= 10;
var += num - 5;
// But:
var *= 10 + num - 5
// Expands to:
var = var * (10 + num - 5);
// Which can be expanded algebraically to:
var = var * (5 + num) = var * 5 + var * num;
```

### 2.1.5 Conditional operators

You can use conditional operators to test conditions. A basic condition follows this structure, given that `?` is a conditional operator and the the whole term is enclosed in a pair of 
