# IndLan

IndLan is a custom programming language with its own syntax — including bilingual English/Hindi keywords — implemented as a tree-walking interpreter in Python.

Made by **Bhavya S Solanki**.

## Run it two ways

### 1. In your browser (no install needed)

Open `playground.html` directly in any browser (just double-click the file, or open it via File → Open). It loads Python in your browser using **Pyodide** (Python compiled to WebAssembly) from a CDN, with IndLan's interpreter embedded right in the page. Write code on the left, click **Run**, see output on the right.

The CDN script is loaded from `https://cdn.jsdelivr.net/pyodide/v0.26.1/full/pyodide.js`, so you need an internet connection the first time you open the page (to fetch the Python runtime). After that, the page itself runs entirely locally — no server, no install, nothing uploaded anywhere.

### 2. On your computer with Python

```bash
python3 indlan.py myprogram.ind     # run a file
python3 indlan.py                   # start an interactive REPL
```

## Project structure

```
indlan/
├── lexer.py             # turns source text into tokens
├── ast_nodes.py          # AST node class definitions
├── ind_parser.py          # recursive-descent parser: tokens -> AST
├── interpreter.py          # tree-walking interpreter: executes the AST
├── indlan.py                # CLI entry point / REPL
├── playground.html           # browser-based runner (Pyodide + CDN)
├── examples_ifelse.ind        # if / elif / else
├── examples_hindi.ind          # Hindi-keyword version of all constructs
└── myprogram.ind                 # simple starter file
```

## Language features

- **Variables**: `let x = 5`
- **Types**: int, float, string, bool, list, dict, null
- **Operators**: `+ - * / %`, `== != < > <= >=`, `and or not`, `+= -= *= /=`
- **Control flow**: `if / elif / else`, `while`, `do { } while`, `for x in range(...)`, `switch / case / default`, `break`, `continue`
- **Functions**: `fun name(params) { ... }`, recursion, closures, first-class functions
- **Classes**: `class Name { fun init(...) {...} fun method(...) {...} }`, instantiated with `new Name(...)`
- **Collections**: lists `[1, 2, 3]` with indexing/mutation, dicts `{"key": value}`
- **Built-ins**: `print`, `len`, `range`, `str`, `int`, `float`, `input`, `type`, `append`, `pop`, `keys`, `values`
- **String methods**: `.upper()`, `.lower()`, `.strip()`, `.split()`
- **Comments**: `// line comment`, `/* block comment */`
- **Error reporting**: every lexer, parser, and runtime error reports the line number
- **Startup banner**: every run shows a welcome box crediting the creator

## Hindi-style keywords

Every keyword in IndLan has a Hindi-style alias that works exactly the same as its English equivalent — use whichever you prefer, or mix both in the same file.

| English | Hindi alias | Meaning |
|---|---|---|
| `let` | `maano` | declare a variable |
| `fun` | `kaam` | declare a function |
| `return` | `vapas` | return a value |
| `if` | `agar` | conditional |
| `elif` | `nahito_agar` | else-if branch |
| `else` | `nahito` | else branch |
| `while` | `jabtak` | while loop |
| `do` | `karo` | do (in do-while) |
| `for` | `pratyek` | for-each loop |
| `in` | `mein` | used in for-loops |
| `switch` | `vibhag` | switch statement |
| `case` | `sthiti` | switch case |
| `default` | `anyatha` | switch default |
| `class` | `varg` | declare a class |
| `new` | `naya` | instantiate a class |
| `this` | `yeh` | reference to current instance |
| `true` | `sahi` | boolean true |
| `false` | `galat` | boolean false |
| `null` | `khaali` | null value |
| `and` | `aur` | logical and |
| `or` | `ya` | logical or |
| `not` | `nahi` | logical not |
| `break` | `roko` | break out of a loop |
| `continue` | `jaari` | continue to next iteration |
| `print` (built-in) | `chhap` | print to output |

## Examples

### English

```indlan
fun factorial(n) {
    if n <= 1 {
        return 1
    }
    return n * factorial(n - 1)
}

print("factorial(6) =", factorial(6))
```

### Hindi

```indlan
kaam factorial(n) {
    agar n <= 1 {
        vapas 1
    }
    vapas n * factorial(n - 1)
}

chhap("factorial(6) =", factorial(6))
```

### do-while

```indlan
let i = 0
do {
    print("i =", i)
    i += 1
} while i < 3
```

### switch / case

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

### Classes

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

## Architecture (how it works internally)

IndLan follows the same pipeline as real interpreted languages:

1. **Lexer** (`lexer.py`) — scans raw source text character by character and groups it into tokens (`IDENT`, `INT`, `STRING`, `PLUS`, `LBRACE`, etc). Hindi keyword aliases are translated to the same token type as their English equivalent right here, so the parser and interpreter need zero special-casing for Hindi support.
2. **Parser** (`ind_parser.py`) — a recursive-descent parser that consumes tokens and builds an Abstract Syntax Tree (AST), using standard operator-precedence climbing (`assignment -> or -> and -> equality -> comparison -> term -> factor -> unary -> call/postfix -> primary`).
3. **Interpreter** (`interpreter.py`) — walks the AST recursively. Each node type has a corresponding `exec_*` (statement) or `eval_*` (expression) method. Variable scoping is handled by a chain of `Environment` objects (every block/function call creates a new environment whose parent is the enclosing scope) — this is what makes closures work correctly.
4. **Browser playground** (`playground.html`) — embeds the four files above as JavaScript template strings, writes them into Pyodide's in-browser virtual filesystem at page load, then calls the same `tokenize` → `parse` → `Interpreter.run` pipeline directly from JavaScript via Pyodide's Python bridge. Output is captured by redirecting Python's `sys.stdout` to an in-memory buffer and displaying it on the page.

## On ".bss" / native compilation

You originally mentioned wanting `.bss`-segment-style execution. That refers to how *compiled* languages (like C) lay out memory in the final binary: `.text` (code), `.data` (initialized globals), `.bss` (uninitialized globals), `.rodata` (constants).

IndLan as built here is an **interpreter** — it runs your `.ind` source directly without producing a binary, which is how Python, JavaScript, and Ruby work too. To get real `.bss`/`.data`/`.text` segments, IndLan would need a second backend: a compiler stage that translates the AST into x86-64 assembly (or LLVM IR) instead of executing it directly. That's a substantial, separate project — happy to start that as a v2 if you want IndLan to also be ahead-of-time compilable to a native executable.

## Known limitations (intentional v1 scope)

- No module/import system yet (`import` is reserved but unimplemented)
- No inheritance for classes yet (single class body, no `extends`)
- No file I/O built-ins yet
- No exception/try-catch handling yet (runtime errors halt the program with a message)

These are natural next additions — let me know which you'd like next.
