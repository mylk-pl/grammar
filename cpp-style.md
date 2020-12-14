# Mylk Contributor Style Guide for C++


## Feature use
This section contains guidance on which features of C++ should be used or avoided

+ Use `#pragma once` for include guards
+ Place all public items inside the library namespace (`mylk`)
+ Use only a single level of namespacing
+ Use enum classes with a defined representation type
  > e.g. `enum class MyEnum: uint8_t { .. }`
+ Keep generics simple, with just a few parameters
+ Avoid ducktyping
  > Generally, this means one should avoid interacting with generic values beyond copy/move, and where interaction must take place, one should use concepts to verify the existence of the field or associated function you will be utilizing
+ Avoid inheritance/virtuals
  > An example of a possible exception to this rule would be in a read/write abstraction: if it provides a cleaner interface than generics it could be allowed
+ Avoid function overloading and default arguments
  > Exceptions to this rule include the `destroy` function mentioned below, and any similar functions which provide a kind of generic trait-like interface
+ Avoid operator overloads
  > Exceptions to this rule include allowing access to a collection with `[]`, dereferencing a handle type with `*` or `->`, utilizing `++` in an iterator, etc
+ Avoid methods
  > Exceptions to this rule can be made where the desired functionality is not possible to achieve using a free function, such as `begin` and `end` for the iterator interface
+ Do not use exceptions
+ Do not use RTTI
+ Do not use the STL
  > Exceptions to this rule include any headers that allow TMP and are compiled away, such as the type traits header
+ Do not use RAII:
  - No `new`/`delete`
    > Use `malloc` and `free` instead
  - Do not use constructors for complex initialization logic
    > Use a function called `create_my_type`
  - Do not use destructors for teardown logic
    > Create an overload for the `destroy` function for your type
  - Do not overload assignment operators
  - Do not use `std::move` equivalent/related functions
  - Do not use r-value references (`T&&`)
+ Prefer references over pointers
+ Prefer `const`, especially in function signatures
+ Keep macro use and `#define`s to a minimum
  > Prefer `constexpr` and `consteval` over defining
+ Do not use assignment expressions
+ Increment/decrement expressions should only be used at the top level of a statement
+ Do not abuse comma operator semantics
+ Do not utilize implicit casting
  > This includes using and defining user-defined cast operator overloads
+ Do not use c-style casts
+ Avoid const-casting


## Formatting
This section contains guidance on how to format code

+ Use `PascalCase` for type names
+ Use `snake_case` variables and fields
+ Use `SCREAMING_SNAKE_CASE` for constants and macros
+ Macros should be namespaced in c style
  > e.g. `MYLK_MACRO_NAME`
+ Always use a block `{}` for the bodies of statements like `if`, `for` etc
+ Place `{` on the same line as its proceeding keyword/function signature
+ Place `else` on the same line as the proceeding `}`
+ Use trailing commas where applicable
+ Use Unix-style LF for line breaks, not Windows' CRLF
+ Use tabs for indentation
+ Include a trailing new line at the bottom of all files