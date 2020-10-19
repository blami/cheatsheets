# C++
Modern C++ cheatsheet.

NOTE: 🚧 _This document is work in progress_.

## Language
### Literals
``` cpp
255, 0277, 0xb0                         // int (decimal, octal, hexadecimal)
u'U'                                    // unsigned int
123.0, 1.23e2                           // double
'a', '\141', '\x61'                     // char (literal, octal, hexadecimal)
"string"                                // char array (\0 terminated string)
"concatenated" "strings"
R"(/raw/string)"                        // raw string (uninterpreted escapes)
true, false                             // bool
nullptr                                 // pointer with address 0
```
C++14 builtin:
``` cpp
0b10                                    // binary number
"test"s                                 // std::string
1i                                      // complex<double>
2h,3min,4s,5ms,...                      // std::chrono::hours,minutes,...
```
User defined literals MUST start with `_` and map to `operator""`:
``` cpp
// Raw (char, char*, wchar_t...)
operator"" _suf(const char)             // 's'_suf
operator"" _suf(const char*)            // 10_suf
operator"" _suf(const char*, size_t)    // "foo"_suf
// Cooked
operator"" _suf(unsigned long long int) // 10_suf
operator"" _suf(long double)            // 1.2_suf
```

### Enums
Default type is `int` but also can be `bool`, `char`, `short int`, `long int`,
or, `long long int`.
``` cpp
enum struct|class name [:type] [{
  enumerator [= constexpr]
}]
```

<!--
## Tips
- Do not use `float`, use more-precise `double` instead.
- Use `const` everywhere you can from beginning.
- Use `auto` with initialized declarations.
-->
