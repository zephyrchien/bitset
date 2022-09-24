# Bitset

Comptime bitset builder.

## Usage

```zig
make(arg1, arg2)
```

Input 1) accepts:

- string (asidentifier) array
- struct {string, value} array

Input 2) accepts an integer type, which will become the base type of bitset.

Output includes:

- bitset type
- const table
- compression func
- decompression func

## Snippets

Build, typedef:

```zig
const rgb = make(.{ "red", "green", "blue" }, u32);
const Set = rgb.set_t;
const RGB = rgb.Table;
const from = rgb.from_cint;
const into = rgb.into_cint;
```

Use compressed bitset:

```zig
fn init(set: Set) {
    if (set.red) { ... }
    if (set.green) { ... }
}

fn main() {
    init(.{.red = true});
}
```

Use fixed sized constants from table:

```zig
fn init2(cset: c_int) {
    init(from(cset));
}

fn main() {
    init2(RGB.red|RGB.green);
}
```

Integrate with C:

```zig
fn initc(set: Set) {
    libc.extern_init(into(set));
}
```
