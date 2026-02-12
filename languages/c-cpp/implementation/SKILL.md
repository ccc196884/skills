---
name: c-cpp-implementation
description: C/C++ pitfalls — memory leaks, UB, buffer overflows, RAII misuse. Load when writing or reviewing .c/.cpp/.h/.hpp files.
---

# C/C++ Implementation — What Claude Gets Wrong

## Memory Safety (Claude's #1 failure area)
- **Every `malloc`/`new` must have a corresponding `free`/`delete`** — Claude often forgets cleanup on error paths
- Use RAII in C++ (smart pointers) — `std::unique_ptr` by default, `std::shared_ptr` only when shared ownership is real
- **Never use raw `new`/`delete` in modern C++** — use `std::make_unique`, `std::make_shared`
- C: always check `malloc` return for `NULL`
- Buffer overflows: use `strncpy`/`snprintf`, never `strcpy`/`sprintf`

## Undefined Behavior (Claude generates UB regularly)
- **Signed integer overflow is UB** — don't assume wraparound
- Null pointer dereference is UB — check before access
- Use-after-free — Claude sometimes reuses freed memory in error paths
- Uninitialized variables — always initialize, especially in C
- Sequence point violations: `i = i++` is UB

## Modern C++ Patterns (C++17/20)
- `std::optional<T>` over returning `-1` or `nullptr` as sentinel
- `std::string_view` for non-owning string references — but don't store views to temporaries
- Structured bindings: `auto [key, value] = *map.begin()`
- `if constexpr` for compile-time branching
- Range-based for: `for (const auto& item : container)`

## C Patterns
- Opaque pointers for encapsulation (`typedef struct Foo Foo;` in header)
- Error codes as return values, output via pointer parameters
- `const` correctness — especially on pointer parameters

## Build Verification
- C: `gcc -Wall -Wextra -Werror -fsanitize=address,undefined`
- C++: `g++ -Wall -Wextra -Werror -std=c++20 -fsanitize=address,undefined`
- Always build with sanitizers during development
- `valgrind` for memory leak detection
- `clang-tidy` for static analysis
