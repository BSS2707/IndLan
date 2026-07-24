# 🇮🇳 IndLan

> **A bilingual programming language that lets you code in English, Hindi, or both.**

**IndLan** is a custom programming language created by **Bhavya S Solanki**. It features its own syntax, lexer, recursive-descent parser, Abstract Syntax Tree (AST), and tree-walking interpreter — all implemented in Python.

Write programs using familiar English keywords, Hindi-style keywords, or mix both in the same program.

```indlan
kaam greet(name) {
    chhap("Namaste,", name)
}

greet("World")
```

---

## ✨ Features

* 🇬🇧 English and 🇮🇳 Hindi-style keywords
* 🧠 Tree-walking interpreter
* 🔤 Custom lexer and recursive-descent parser
* 🌳 Abstract Syntax Tree (AST)
* 🔁 Variables, loops, conditions, and functions
* 🧩 Recursion and closures
* 🏛️ Classes and objects
* 📦 Lists and dictionaries
* 🛠️ Built-in functions
* 🖥️ Interactive REPL
* 🌐 Browser playground powered by Pyodide
* 📍 Line-numbered lexer, parser, and runtime errors
* 🎉 Startup banner with creator credit

---

# 🚀 Run IndLan

## 1. Install from PyPI

```bash
pip install indlan
```

## Run a program

```bash
indlan myprogram.ind
```

## Start the interactive REPL

```bash
indlan
```

Example:

```text
$ indlan

╔══════════════════════════════════════╗
║        Welcome to IndLan 🇮🇳         ║
║     Created by Bhavya S Solanki      ║
╚══════════════════════════════════════╝

>>
```

---

## 2. Run in Your Browser

No installation required.

Open:

```text
playground.html
```

You can either:

* Double-click the file
* Open it using **File → Open** in your browser

The browser playground uses **Pyodide**, which runs Python directly inside WebAssembly.

The first time you open the playground, an internet connection is required to load the Python runtime. After that, the IndLan interpreter runs locally inside your browser.

```text
┌──────────────────────┬──────────────────────┐
│   IndLan Code        │      Output           │
│                      │                      │
│   let x = 10         │   10                 │
│   print(x)           │                      │
│                      │                      │
│       [ Run ]        │                      │
└──────────────────────┴──────────────────────┘
```

---

# 📁 Project Structure

```text
indlan/
├── lexer.py              # Source code → Tokens
├── ast_nodes.py          # AST node definitions
├── ind_parser.py         # Tokens → AST
├── interpreter.py         # AST execution
├── indlan.py              # CLI and REPL
├── playground.html        # Browser-based playground
│
├── examples_ifelse.ind    # if / elif / else example
├── examples_hindi.ind     # Hindi keyword examples
└── myprogram.ind          # Starter program
```

---

# 🧑‍💻 Language Syntax

## Variables

```indlan
let name = "Bhavya"
let age = 19
```

Hindi-style:

```indlan
maano naam = "Bhavya"
maano umar = 19
```

---

## Data Types

IndLan supports:

```text
int
float
string
bool
list
dict
null
```

Example:

```indlan
let age = 19
let price = 99.99
let name = "IndLan"
let active = true
let numbers = [1, 2, 3]
let user = {"name": "Bhavya"}
let value = null
```

---

# 🔀 Control Flow

## If / Elif / Else

```indlan
let age = 19

if age >= 18 {
    print("Adult")
} elif age >= 13 {
    print("Teenager")
} else {
    print("Child")
}
```

Hindi version:

```indlan
maano umar = 19

agar umar >= 18 {
    chhap("Adult")
} nahito_agar umar >= 13 {
    chhap("Teenager")
} nahito {
    chhap("Child")
}
```

---

## While Loop

```indlan
let i = 0

while i < 5 {
    print(i)
    i += 1
}
```

Hindi:

```indlan
maano i = 0

jabtak i < 5 {
    chhap(i)
    i += 1
}
```

---

## Do-While Loop

```indlan
let i = 0

do {
    print("i =", i)
    i += 1
} while i < 3
```

---

## For Loop

```indlan
for i in range(5) {
    print(i)
}
```

Hindi:

```indlan
pratyek i mein range(5) {
    chhap(i)
}
```

---

## Break and Continue

```indlan
while true {
    if condition {
        break
    }

    continue
}
```

Hindi:

```indlan
jabtak sahi {
    agar condition {
        roko
    }

    jaari
}
```

---

# 🔀 Switch / Case

```indlan
let day = 3

switch day {
    case 1 {
        print("Monday")
    }

    case 3 {
        print("Wednesday")
    }

    default {
        print("Some other day")
    }
}
```

Hindi version:

```indlan
maano din = 3

vibhag din {
    sthiti 1 {
        chhap("Monday")
    }

    sthiti 3 {
        chhap("Wednesday")
    }

    anyatha {
        chhap("Some other day")
    }
}
```

---

# 🧩 Functions

```indlan
fun greet(name) {
    print("Hello", name)
}

greet("Bhavya")
```

Hindi:

```indlan
kaam abhivaadan(naam) {
    chhap("Namaste", naam)
}

abhivaadan("Bhavya")
```

---

## Recursion

```indlan
fun factorial(n) {
    if n <= 1 {
        return 1
    }

    return n * factorial(n - 1)
}

print(factorial(6))
```

Hindi:

```indlan
kaam factorial(n) {
    agar n <= 1 {
        vapas 1
    }

    vapas n * factorial(n - 1)
}

chhap(factorial(6))
```

Output:

```text
720
```

---

# 🏛️ Classes and Objects

```indlan
class Animal {
    fun init(name, sound) {
        this.name = name
        this.sound = sound
    }

    fun speak() {
        print(this.name, "says", this.sound)
    }
}

let dog = new Animal("Dog", "Woof")

dog.speak()
```

Hindi-style:

```indlan
varg Pashu {
    kaam init(naam, awaaz) {
        yeh.naam = naam
        yeh.awaaz = awaaz
    }

    kaam bolo() {
        chhap(yeh.naam, "kehta hai", yeh.awaaz)
    }
}

maano kutta = naya Pashu("Dog", "Woof")

kuttta.bolo()
```

---

# 📦 Collections

## Lists

```indlan
let numbers = [1, 2, 3]

print(numbers[0])

append(numbers, 4)

print(len(numbers))
```

## Dictionaries

```indlan
let user = {
    "name": "Bhavya",
    "language": "IndLan"
}

print(user["name"])
```

---

# 🛠️ Built-in Functions

| Function   | Description               |
| ---------- | ------------------------- |
| `print()`  | Print output              |
| `chhap()`  | Hindi alias for `print()` |
| `len()`    | Get length                |
| `range()`  | Generate a range          |
| `str()`    | Convert to string         |
| `int()`    | Convert to integer        |
| `float()`  | Convert to float          |
| `input()`  | Read user input           |
| `type()`   | Get value type            |
| `append()` | Add to a list             |
| `pop()`    | Remove from a list        |
| `keys()`   | Get dictionary keys       |
| `values()` | Get dictionary values     |

---

# 🔤 Hindi Keyword Support

Every major keyword has a Hindi-style alias.

| English    | Hindi Alias   | Purpose              |
| ---------- | ------------- | -------------------- |
| `let`      | `maano`       | Variable declaration |
| `fun`      | `kaam`        | Function             |
| `return`   | `vapas`       | Return value         |
| `if`       | `agar`        | Condition            |
| `elif`     | `nahito_agar` | Else-if              |
| `else`     | `nahito`      | Else                 |
| `while`    | `jabtak`      | While loop           |
| `do`       | `karo`        | Do-while             |
| `for`      | `pratyek`     | For loop             |
| `in`       | `mein`        | Collection iteration |
| `switch`   | `vibhag`      | Switch statement     |
| `case`     | `sthiti`      | Case                 |
| `default`  | `anyatha`     | Default case         |
| `class`    | `varg`        | Class                |
| `new`      | `naya`        | Create object        |
| `this`     | `yeh`         | Current object       |
| `true`     | `sahi`        | Boolean true         |
| `false`    | `galat`       | Boolean false        |
| `null`     | `khaali`      | Null                 |
| `and`      | `aur`         | Logical AND          |
| `or`       | `ya`          | Logical OR           |
| `not`      | `nahi`        | Logical NOT          |
| `break`    | `roko`        | Stop loop            |
| `continue` | `jaari`       | Continue loop        |
| `print`    | `chhap`       | Print output         |

You can even mix both languages:

```indlan
maano age = 20

if age >= 18 {
    chhap("Adult")
} nahito {
    print("Minor")
}
```

---

# 🧠 How IndLan Works

IndLan follows the same fundamental architecture used by real programming languages.

```text
Source Code
     │
     ▼
┌─────────────┐
│    Lexer    │
└──────┬──────┘
       │ Tokens
       ▼
┌─────────────┐
│    Parser   │
└──────┬──────┘
       │ AST
       ▼
┌─────────────┐
│ Interpreter  │
└──────┬──────┘
       │
       ▼
    Output
```

### 1. Lexer

The lexer reads source code character by character and converts it into tokens.

```text
let x = 10
```

Becomes something like:

```text
LET IDENTIFIER EQUALS INTEGER
```

Hindi keywords are converted to the same internal token as their English equivalents.

For example:

```text
let   → LET
maano → LET
```

This means the parser does not need special Hindi-language logic.

---

### 2. Parser

The parser uses recursive descent to convert tokens into an Abstract Syntax Tree.

Operator precedence is handled through:

```text
assignment
    ↓
or
    ↓
and
    ↓
equality
    ↓
comparison
    ↓
term
    ↓
factor
    ↓
unary
    ↓
call / postfix
    ↓
primary
```

---

### 3. Interpreter

The interpreter walks through the AST and executes the program.

Each AST node has a corresponding operation such as:

```text
exec_*  → Statements
eval_*  → Expressions
```

Variable scopes are managed using chained `Environment` objects.

This enables:

* Block scope
* Function scope
* Closures
* Recursive functions

---

# 🌐 Browser Architecture

The browser playground uses **Pyodide** to run Python inside the browser.

The process is:

```text
IndLan Source Code
        │
        ▼
JavaScript Playground
        │
        ▼
Pyodide
        │
        ▼
Python Virtual Filesystem
        │
        ▼
Lexer → Parser → Interpreter
        │
        ▼
Output Panel
```

The same interpreter pipeline is used:

```text
tokenize()
    ↓
parse()
    ↓
Interpreter.run()
```

Program output is captured and displayed directly in the browser.

---

# 🧪 Example Program

```indlan
class Calculator {
    fun add(a, b) {
        return a + b
    }

    fun multiply(a, b) {
        return a * b
    }
}

let calc = new Calculator()

print("Addition:", calc.add(10, 20))
print("Multiplication:", calc.multiply(5, 6))
```

Output:

```text
Addition: 30
Multiplication: 30
```

---

# ⚙️ Current Limitations

The current v1 release intentionally does not include:

* ❌ Module/import system
* ❌ Class inheritance
* ❌ File I/O
* ❌ Exception handling
* ❌ `try / catch`
* ❌ Native compilation

These features are planned possibilities for future versions.

---

# 🚀 Future Roadmap

Possible future versions may include:

* [ ] Module and package system
* [ ] `import` support
* [ ] Class inheritance
* [ ] `try / catch` exception handling
* [ ] File I/O
* [ ] Standard library
* [ ] Package manager
* [ ] Bytecode virtual machine
* [ ] JIT compilation
* [ ] Native compiler backend
* [ ] x86-64 assembly generation
* [ ] LLVM backend
* [ ] `.text`, `.data`, `.bss`, and `.rodata` segment support

---

# 🧱 About Native Compilation

IndLan is currently an **interpreted language**.

It executes:

```text
.ind Source Code
        ↓
      Lexer
        ↓
      Parser
        ↓
       AST
        ↓
  Tree-Walking Interpreter
        ↓
      Output
```

A future compiler backend could instead generate:

```text
.ind Source Code
        ↓
      Lexer
        ↓
      Parser
        ↓
       AST
        ↓
   Compiler Backend
        ↓
  Assembly / LLVM IR
        ↓
   Native Executable
```

This could eventually enable real native executable generation with memory sections such as:

```text
.text   → Machine code
.data   → Initialized global data
.bss    → Uninitialized global data
.rodata → Read-only constants
```

That would be a major **IndLan v2** direction.

---

# 👨‍💻 Creator

## Bhavya S Solanki

**AI/ML Student • Python Developer • Data Scientist • Programming Language Creator**

IndLan is an experimental programming language project built to explore:

* Compiler design
* Lexical analysis
* Parsing
* Abstract Syntax Trees
* Interpreters
* Programming language architecture
* Bilingual programming syntax

---

# 📜 License

Add your preferred license here, such as:

```text
MIT License
```

---

⭐ If you like the idea of programming in both English and Hindi, consider starring the project!

**IndLan — Code your way. अपनी भाषा में कोड करो।**
