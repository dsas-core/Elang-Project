## Elang — Complete Syntax & Keywords Reference

---

## 1. Keywords

### Core Keywords
```
let        mut        func       async      return
if         elif       else       while      for
in         use        type       match      
try        catch      break      continue
spawn      channel    send       receive
and        or         not        await      pub
true       false      none       unsafe     extern
```

### Built-in Functions
```
print      show       display    input
read       write      append     
fetch      download   
sleep      timeout    
exists     mkdir      listdir    
env        setenv     
```

### Built-in Modules
```
sys        path       time       random
json       hash       base64     log
```

---

## 2. Data Types

### Primitive Types
```elang
int         -- 64-bit signed integer
int8        -- -128 to 127
int16       -- -32768 to 32767
int32       -- -2147483648 to 2147483647
int64       -- same as int
uint        -- 64-bit unsigned
uint8       -- 0 to 255
uint16      -- 0 to 65535
uint32      -- 0 to 4294967295
uint64      -- 0 to 18446744073709551615
float       -- 64-bit decimal (f64)
float32     -- 32-bit decimal
float64     -- same as float
bool        -- true / false
char        -- Unicode codepoint ('a'')
str         -- UTF-8 string
none        -- null/nil equivalent
```

### Compound Types
```elang
[]int               -- slice (dynamic array)
[5]int              -- fixed array (size 5)
map[str]int         -- hash map
(int, str, bool)    -- tuple
int?                -- optional (nullable)
Result[int, str]    -- result type (ok or error)
func(int, int) int  -- function type
channel[int]        -- concurrent channel
```

---

## 3. Variables

```elang
-- Immutable
let name = "Elang"
let version int = 1
let pi float = 3.14

-- Mutable
mut count = 0
mut name str = "David"

-- Multiple assignment
let x, y = 10, 20
let (a, b) = (1, 2)

-- Destructuring tuple
let (q, r) = divmod(10, 3)

-- Shadowing
let x = 5
let x = x * 2      -- new x, value 10

-- Type inference
let nums = [1, 2, 3]        -- []int
let data = map{"a": 1}      -- map[str]int
```

---

## 4. Literals

```elang
-- Integer
42
-10
0
1_000_000       -- underscore separator
0xFF            -- hexadecimal
0b1010          -- binary
0o17            -- octal

-- Float
3.14
-0.5
1.5e10
2.5e-3

-- String
"Hello World"
"Line1\nLine2"
"Tab\there"
"Quote\"here"
"Path\\file"

-- String interpolation
"Hello {name}!"
"Sum: {a + b}"
"Upper: {name.upper()}"
"Pi = {pi:.2f}"

-- Char
'a'
'Z'
'ক'
'\n'
'\t'
'\u0041'        -- Unicode: 'A'

-- Boolean
true
false

-- None
none

-- Array
[1, 2, 3]
["apple", "banana"]
[[1,2], [3,4]]      -- 2D

-- Map
map{"key": "value"}
map{"name": "David", "age": 25}

-- Tuple
(10, 20)
("David", 25, true)

-- Range
0..10           -- 0 to 9 (exclusive)
0..=10          -- 0 to 10 (inclusive)
'a'..='z'       -- char range
```

---

## 5. Operators

### Arithmetic
```elang
+       -- Addition
-       -- Subtraction
*       -- Multiplication
/       -- Division
%       -- Modulo (Remainder)
**      -- power (2**10 = 1024)
-x      -- unary minus
```

### Comparison
```elang
==      -- Equal to 
!=      -- Not Equal to 
<       -- Less than
>       -- Greater than 
<=      -- Less than or equal to
>=      -- Greater than or equal to 
```

### Logical
```elang
and     -- AND (&&)
or      -- OR (||)
not     -- NOT (!)
```

### Assignment
```elang
=       -- assign
+=      -- add and assign
-=      -- subtract and assign
*=      -- multiply and assign
/=      -- divide and assign
%=      -- modulo and assign
```

### String
```elang
++      -- concatenation ("Hello" ++ " World")
```

### Special
```elang
..      -- exclusive range
..=     -- inclusive range
|>      -- pipe (f |> g = g(f))
??      -- null coalescing (x ?? "default")
?       -- optional chaining (obj?.field)
!       -- force unwrap (x!)
=>      -- arrow (match arms, lambda)
::      -- scope resolution
```

### Precedence (Top = Highest)
```
9  →  |>
8  →  ** (right-associative)
7  →  * / %
6  →  + - ++
5  →  .. ..=
4  →  == != < > <= >=
3  →  not
2  →  and
1  →  or
```

---

## 6. Functions

```elang
-- Basic
func greet(name str)
    print "Hello, {name}!"

-- With return type
func add(a int, b int) int
    return a + b

-- Multiple return
func divmod(a int, b int) (int, int)
    return a / b, a % b

-- Default parameter
func greet(name str, greeting str = "Hello")
    print "{greeting}, {name}!"

-- Named arguments
createUser(name: "David", age: 25, city: "Los Angeles ")

-- Variadic
func sum(nums ...int) int
    mut total = 0
    for n in nums
        total += n
    return total

-- Generic
func first[T](items []T) T?
    if items.len == 0
        return none
    return items[0]

-- Async
async func fetchData(url str) str
    let res = await fetch(url)
    return res.body

-- Lambda (inline)
let double = func(x int) int => x * 2

-- Lambda (block)
let add = func(a int, b int) int =>
    return a + b

-- Higher order
let nums = [1, 2, 3, 4, 5]
let doubled  = nums.map(func(x int) int => x * 2)
let evens    = nums.filter(func(x int) bool => x % 2 == 0)
let total    = nums.reduce(0, func(acc int, x int) int => acc + x)

-- Pipe operator
let result = "  hello world  "
    |> trim
    |> toUpper
    |> split(" ")

-- Recursive
func factorial(n int) int
    if n <= 1
        return 1
    return n * factorial(n - 1)

-- Method
func Point.distance(self) float
    return (self.x ** 2 + self.y ** 2) ** 0.5

-- Mut method
func Counter.increment(mut self)
    self.value += 1

-- Public
pub func exported(x int) int
    return x * 2
```

---

## 7. Control Flow

### if / elif / else
```elang
if x > 10
    print "big"
elif x == 10
    print "equal"
else
    print "small"

-- Single line
if flag then print "yes" else print "no"

-- if expression
let grade = if score >= 90 then "A" elif score >= 80 then "B" else "C"

-- if let (optional unwrap)
if let value = maybeValue
    print "Got: {value}"
```

### while
```elang
while count < 10
    count += 1

-- Infinite loop
while true
    let input = input "Command: "
    if input == "quit"
        break

-- Labeled
outer: while true
    while true
        break outer
```

### for
```elang
-- Range
for i in 0..10
    print i

for i in 0..=10
    print i

-- Collection
for item in list
    print item

-- With index
for i, item in list.enumerate()
    print "{i}: {item}"

-- Map
for key, value in myMap
    print "{key} = {value}"

-- Reverse
for i in 10..0
    print i

-- Step (via range filter)
for i in (0..20).step(2)
    print i

-- Labeled
outer: for i in 0..5
    for j in 0..5
        if i + j == 6
            break outer
```

### match
```elang
-- Basic
match day
    1 => print "Saturday"
    2 => print "Sunday"
    _ => print "Weekday"

-- Range pattern
match score
    90..=100 => print "A+"
    80..89   => print "A"
    _        => print "F"

-- Enum pattern
match direction
    Direction.North => move_up()
    Direction.South => move_down()
    Direction.East  => move_right()
    Direction.West  => move_left()

-- With data
match shape
    Shape.Circle(r)       => print 3.14 * r * r
    Shape.Rect(w, h)      => print w * h
    Shape.Triangle(b, h)  => print 0.5 * b * h

-- Guard (when condition)
match x
    n when n < 0  => print "negative"
    n when n == 0 => print "zero"
    n             => print "positive: {n}"

-- Multiple patterns
match c
    'a' | 'e' | 'i' | 'o' | 'u' => print "vowel"
    _                             => print "consonant"

-- match expression (returns value)
let label = match code
    200 => "OK"
    404 => "Not Found"
    500 => "Server Error"
    _   => "Unknown"

-- Tuple match
match (x, y)
    (0, 0) => print "origin"
    (x, 0) => print "x-axis"
    (0, y) => print "y-axis"
    (x, y) => print "point"
```

---

## 8. Custom Types

### Struct-like
```elang
type Point
    x float
    y float

type Person
    name str
    age  int
    city str = "Los Angeles "      -- default value

-- Created
let p = Point(x: 3.0, y: 4.0)
let r = Person(name: "David", age: 25)

-- Access
print p.x
print r.name

-- Update (mut)
mut p2 = Point(x: 0.0, y: 0.0)
p2.x = 5.0
```

### Enum
```elang
type Direction
    | North
    | South
    | East
    | West

type Shape
    | Circle(radius float)
    | Rectangle(width float, height float)
    | Triangle(base float, height float)

type Result[T, E]
    | Ok(value T)
    | Err(error E)

-- Use
let d = Direction.North
let s = Shape.Circle(radius: 5.0)
let r = Result.Ok(42)
```

### Methods
```elang
type Rectangle
    width  float
    height float

func Rectangle.area(self) float
    return self.width * self.height

func Rectangle.scale(mut self, factor float)
    self.width  *= factor
    self.height *= factor

func Rectangle.new(w float, h float) Rectangle
    return Rectangle(width: w, height: h)

-- Use
let rect = Rectangle.new(5.0, 3.0)
print rect.area()
```

### Interface
```elang
type Drawable
    func draw(self)
    func resize(mut self, factor float)

type Printable
    func toString(self) str

-- Implementation 
type Circle
    radius float

func Circle.draw(self)
    print "Circle r={self.radius}"

func Circle.resize(mut self, f float)
    self.radius *= f

-- As Interface type
func render(shape Drawable)
    shape.draw()
```

### Generics
```elang
type Stack[T]
    items []T

func Stack[T].push(mut self, item T)
    self.items.add(item)

func Stack[T].pop(mut self) T?
    if self.items.len == 0
        return none
    return self.items.removeLast()

func Stack[T].peek(self) T?
    if self.items.len == 0
        return none
    return self.items[self.items.len - 1]

-- Use
mut s = Stack[int](items: [])
s.push(1)
s.push(2)
print s.pop()    -- 2
```

---

## 9. Error Handling

```elang
-- try / catch
try
    let file = read("data.txt")
    print file
catch FileNotFound as err
    print "File নেই: {err.message}"
catch PermissionError
    print "Permission denied"
catch err
    print "Error: {err}"

-- Result type
func divide(a float, b float) Result[float, str]
    if b == 0.0
        return Err("Division by zero is not possible.")
    return Ok(a / b)

match divide(10.0, 2.0)
    Ok(v)  => print v
    Err(e) => print "Error: {e}"

-- ? operator (error propagation)
func calculate() Result[float, str]
    let x = divide(10.0, 2.0)?   -- Return on Error
    let y = divide(x, 3.0)?
    return Ok(y)

-- Optional handling
let name str? = none
print name ?? "default"     -- "default"
print name!                 -- force unwrap (crash if none)

if name != none
    print name!

-- if let
if let n = name
    print "Got: {n}"
else
    print "Empty"
```

---

## 10. Concurrency

```elang
-- spawn
spawn func()
    print "background task"

-- spawn with result
let task = spawn func() int =>
    return heavyComputation()

let result = await task

-- channel
let ch = channel[int]()
let ch = channel[str](capacity: 10)   -- buffered

-- send / receive
spawn func()
    send ch 42
    send ch 99
    ch.close()

-- receive one
let val = receive ch

-- receive in loop
for val in ch
    print val

-- select (multiple channels)
select
    val from ch1 => print "ch1: {val}"
    val from ch2 => print "ch2: {val}"
    timeout(1.0) => print "timeout"

-- mutex
let counter = mutex[int](0)
counter.lock() do mut c =>
    c += 1

-- async / await
async func fetchAll(urls []str) []str
    let tasks = urls.map(func(url str) => spawn fetch(url))
    let results = await all(tasks)
    return results.map(func(r) => r.body)

-- async main
async func main()
    let data = await fetchData("https://api.example.com")
    print data
```

---

## 11. Modules

```elang
-- Import
use math
use io
use net.http
use net.http as http
use io.{readFile, writeFile}
use collections.{List, Map, Set}

-- Public export
pub func myFunction()
    print "exported"

pub type MyType
    value int

-- Package structure
myapp/
    main.el
    elang.pkg
    src/
        utils.el
        models.el
    tests/
        test_utils.el
```

---

## 12. Built-in Primitives (Zero Import)

### Network
```elang
let res  = fetch("https://api.example.com")
let data = fetch.json("https://api.example.com/users")
let res  = fetch("https://api.example.com",
    method:  "POST",
    body:    "{\"name\":\"David\"}",
    headers: {"Content-Type": "application/json"}
)
print res.status
print res.body

download("https://example.com/file.zip", to: "file.zip")
```

### Timing
```elang
sleep(3)
sleep(0.5)
sleep(ms: 200)
sleep(min: 1)

let t = timer.start()
sleep(1)
print t.elapsed()
print t.ms()

timeout(5) do
    let res = fetch("https://slow.com")
catch TimeoutError
    print "Too slow!"
```

### System
```elang
sys.run("ls -la")
sys.run("mkdir", "-p", "output")

let out  = sys.capture("ls")
let res  = sys.exec("ping -c 1 google.com")
let proc = sys.spawn("python3 server.py")

print sys.os        -- "linux" / "macos" / "windows"
print sys.arch      -- "x86_64" / "arm64"
print sys.cpus      -- 8
print sys.hostname
print sys.username
print sys.pid
print sys.cwd()
sys.chdir("src/")
```

### File System
```elang
let text = read("file.txt")
write("out.txt", "content")
append("log.txt", "line\n")

exists("file.txt")        -- bool
isfile("readme.md")       -- bool
isdir("src/")             -- bool
filesize("video.mp4")     -- int

mkdir("output/logs")
listdir("src/")           -- []str
copyfile("a.txt", "b.txt")
movefile("old.txt", "new.txt")
deletefile("temp.txt")

path.join("src", "main.el")   -- "src/main.el"
path.ext("file.tar.gz")       -- ".gz"
path.base("src/main.el")      -- "main.el"
path.dir("src/main.el")       -- "src"
path.abs("../config.json")
```

### Environment
```elang
let home = env("HOME")
let port = env("PORT") ?? "8080"
setenv("DEBUG", "true")
let args = sys.args
```

### Time
```elang
let now = time.now()
print now.year
print now.month
print now.day
print now.hour
print now.minute
print now.second
print now.weekday
print now.format("YYYY-MM-DD")
print now.unix()

let tomorrow = now + time.days(1)
let diff = time.diff(now, tomorrow)
print diff.hours
```

### Random
```elang
random.int(1, 100)
random.float(0.0, 1.0)
random.bool()
random.choice(["a", "b", "c"])
random.shuffle([1, 2, 3, 4, 5])
random.uuid()
random.hex(16)
random.seed(42)
```

### JSON
```elang
let obj = json.parse("{\"name\": \"Elang\"}")
print obj["name"]

let text = json.stringify(data)
let text = json.pretty(data)

-- Type-safe parse
let config = json.parse[Config](text)
```

### Hash / Encode
```elang
hash.md5("hello")
hash.sha256("password")
hash.sha512(data)
hash.hmac("secret", "message", algo: "sha256")

base64.encode("Hello World")
base64.decode(encoded)
base64.url_encode(data)
```

### Print Advanced
```elang
print.red("Error!")
print.green("Success!")
print.yellow("Warning!")
print.blue("Info")
print.bold("Important")
print.dim("subtle")

print.table([
    ["Name",  "Age"],
    ["David", "25"],
    ["Riyan", "30"],
])

print.progress(50, 100, label: "Loading")
print.noln "Enter: "
print.debug someVar
print.fmt "{:.2f}" 3.14159
```

---

## 13. C FFI

```elang
-- Extern C functions
extern "C"
    func malloc(size int) *void
    func free(ptr *void)
    func strlen(s *char) int
    func printf(fmt *char, ...) int

-- Opaque C types
extern "C"
    type FILE
    type SQLite3

-- Unsafe block (pointer access)
unsafe
    let ptr = malloc(1024)
    memcpy(ptr, src, 1024)
    free(ptr)

-- Link to C library
#link "sqlite3"
#link "curl"
#include "sqlite3.h"

extern "C"
    func sqlite3_open(filename str, db **SQLite3) int
    func sqlite3_exec(db *SQLite3, sql str) int
    func sqlite3_close(db *SQLite3) int
```

---

## 14. elp — Package Manager

```bash
elp install sqlite
elp install sqlite@3.40.1
elp install sqlite curl sdl2
elp remove sqlite
elp update
elp update sqlite
elp search database
elp info sqlite
elp list
elp publish
elp login
elp init
elp init --lib
elp build
elp run
elp test
elp clean
elp audit
elp outdated
```

---

## 15. Comments

```elang
-- This is single-line comment

For multi-line, use -- on every line
-- This line is also a comment
-- This line is also a comment

let x = 10  -- inline comment
```

---

## 16. Special Syntax

```elang
-- String formatting
"{value}"             -- basic
"{value:.2f}"         -- float precision
"{value:>10}"         -- right align
"{value:<10}"         -- left align
"{value:^10}"         -- center
"{value:0>5}"         -- zero pad
"{value:x}"           -- hex
"{value:b}"           -- binary

-- Conditional expression
let x = if cond then a else b

-- do block
counter.lock() do mut c =>
    c += 1

timeout(5) do
    fetch("https://api.com")

-- Spread (variadic call)
let args = [1, 2, 3]
sum(...args)

-- Type assertion
let n = value as int
let s = value as str

-- Null safety chain
user?.address?.city ?? "Unknown"

-- Force unwrap
let val = optional!

-- Result propagation
let result = riskyOperation()?
```

---

## Complete Example — All features together

```elang
use net.http

type User
    | Admin(name str, level int)
    | Regular(name str, email str)
    | Guest

async func fetchUser(id int) Result[User, str]
    try
        let res = await fetch("https://api.example.com/users/{id}")
        let data = json.parse(res.body)

        match data["role"]
            "admin"   => return Ok(User.Admin(
                            name:  data["name"],
                            level: data["level"].toInt() ?? 1
                         ))
            "regular" => return Ok(User.Regular(
                            name:  data["name"],
                            email: data["email"]
                         ))
            _         => return Ok(User.Guest)
    catch NetworkError as e
        return Err("Network failed: {e.message}")
    catch err
        return Err("Unknown error: {err}")

async func main()
    for id in 1..=5
        match await fetchUser(id)
            Ok(User.Admin(name, level)) =>
                print.green("Admin: {name} (Level {level})")
            Ok(User.Regular(name, email)) =>
                print.blue("User: {name} <{email}>")
            Ok(User.Guest) =>
                print.dim("Guest user")
            Err(msg) =>
                print.red("Error: {msg}")
        sleep(ms: 100)
```

---

