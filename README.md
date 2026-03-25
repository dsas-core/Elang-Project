<div align="center">

<img src="https://raw.githubusercontent.com/dsas-core/Elang-Project/refs/heads/main/assets/elang.png" alt="Elang Logo" width="160" />

# ELANG

### The Falcon Programming Language

*Simple as Python · Safe as Rust · Fast as C*

[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)]()
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)]()
[![Stars](https://img.shields.io/github/stars/dsas-core/Elang-Project?style=social)]()

</div>

---
---
# Currently under development
---
## Introduction

Modern programming forces a painful trade-off. You either write **simple code that is slow**, or **fast code that is complex and unsafe**. Python is easy to read but too slow for systems work. C is fast but dangerous. Rust is safe but notoriously hard to learn.

**Elang** was created to break this trade-off.

Elang (Indonesian: *Elang*, English: *Falcon*) is a compiled, statically-typed, self-hosted programming language that gives you Python-level simplicity, Rust-level memory safety, and C-level performance — all in one language. Write clean, readable code and get a native binary with zero runtime overhead.

One language. Every domain.

---

## Goals & Vision

Elang is built around four uncompromising goals:

**Simplicity** — Code should read like plain English. No cryptic symbols, no excessive punctuation, no boilerplate. If a beginner cannot read your code on day one, the language has failed.

**Safety** — Memory errors, null pointer crashes, and data races should be impossible by default. The compiler catches mistakes before they become production incidents.

**Performance** — Elang compiles directly to native machine code. No virtual machine, no garbage collector pauses, no interpreter overhead. Programs run at the speed of C.

**Universality** — One language should be enough. Backend APIs, GUI applications, system programs, operating systems, AI systems — Elang targets them all without compromise.

The long-term vision is a language that is self-hosted (the compiler is written in Elang itself), has a rich standard library written entirely in Elang, and powers a growing ecosystem through its package manager `elp`.

---

## Key Features

**Indentation-based syntax** — Elang uses indentation to define blocks, like Python. No curly braces, no `end` keywords, no semicolons. The structure of your code is visible at a glance.

**Type inference** — Elang is statically typed, but you rarely need to write types. The compiler figures them out. You get the safety of static typing with the feel of dynamic typing.

**Ownership-based memory management** — Memory is managed at compile time using an ownership model. No garbage collector, no manual `malloc`/`free`, no memory leaks.

**Auto syntax correction** — The compiler detects and automatically fixes common mistakes before compiling. Missing semicolons, wrong capitalization, Python-style print calls — all corrected with a warning.

**Built-in concurrency** — `spawn`, `channel`, `send`, `receive`, and `async`/`await` are keywords, not library calls. Concurrency is a first-class citizen.

**Zero-import primitives** — HTTP requests, file I/O, system commands, JSON parsing, sleep, random numbers — all available without any import statement.

**C FFI** — Call any C library directly using `extern "C"` blocks. The entire C ecosystem is available to Elang programs.

**Self-hosted compiler** — The Elang compiler is written in Elang. The language builds itself.

---

## Getting Started

Source files use the `.el` extension.

```elang
-- hello.el
func main()
    print "Hello, World!"
```

Compile and run:

```bash
elang hello.el          -- compile → a.out
elang --run hello.el    -- compile and run immediately
elang --check hello.el  -- type-check only, no output
```

---

## Code Examples

### Variables

```elang
let name    = "Elang"       -- immutable
mut count   = 0             -- mutable
let pi float = 3.14159

count += 1
```

### Functions

```elang
func add(a int, b int) int
    return a + b

func greet(name str, greeting str = "Hello")
    print "{greeting}, {name}!"

async func fetchData(url str) str
    let res = await fetch(url)
    return res.body
```

### Control Flow

```elang
if score >= 90
    print "A+"
elif score >= 80
    print "A"
else
    print "Try again"

for i in 0..10
    print i

while count < 5
    count += 1

match direction
    Direction.North => move_up()
    Direction.South => move_down()
    _               => print "unknown"
```

### Types

```elang
type Point
    x float
    y float

func Point.distance(self) float
    return (self.x ** 2 + self.y ** 2) ** 0.5

let p = Point(x: 3.0, y: 4.0)
print p.distance()    -- 5.0
```

### Enum

```elang
type Shape
    | Circle(radius float)
    | Rectangle(width float, height float)

let area = match shape
    Shape.Circle(r)       => 3.14 * r * r
    Shape.Rectangle(w, h) => w * h
```

### Error Handling

```elang
func divide(a float, b float) Result[float, str]
    if b == 0.0
        return Err("division by zero")
    return Ok(a / b)

match divide(10.0, 2.0)
    Ok(v)  => print "Result: {v}"
    Err(e) => print "Error: {e}"
```

### Concurrency

```elang
let ch = channel[int]()

spawn func()
    for i in 1..=5
        send ch i
    ch.close()

for val in ch
    print val
```

### Built-in Primitives

```elang
-- HTTP (no import needed)
let res  = fetch("https://api.example.com")
let data = fetch.json("https://api.example.com/users")

-- File I/O (no import needed)
let text = read("data.txt")
write("output.txt", "Hello World")

-- System (no import needed)
sys.run("ls -la")
let out = sys.capture("git log --oneline")

-- Sleep (no import needed)
sleep(1)
sleep(ms: 500)

-- JSON (no import needed)
let obj = json.parse(text)
let str = json.pretty(data)
```

### C FFI

```elang
extern "C"
    func sqlite3_open(filename str, db **SQLite3) int
    func sqlite3_exec(db *SQLite3, sql str) int
    func sqlite3_close(db *SQLite3) int
    type SQLite3

unsafe
    let db = sqlite3_open("app.db")
    sqlite3_exec(db, "CREATE TABLE users (id INT, name TEXT)")
    sqlite3_close(db)
```

### Package Manager

```bash
elp install sqlite
elp install sqlite curl sdl2
elp search database
elp update
elp publish
```

---
## Grammer
[Grammer.md](Grammer.md)

---
## License

MIT © Elang Contributors — see [LICENSE](LICENSE) for details.

---

<div align="center">

*"A language that gets out of your way and lets you build."*

</div>
