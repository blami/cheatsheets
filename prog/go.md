# Go
Golang cheatsheet.

NOTE: 🚧 _This document is work in progress_.

## Language
### Variables and Constants
``` go
var x int
var x int = 1
x := 1                  // induced type
const x = 1

num := 1                // int
num := 1.               // float64
num := 1 + 2i           // complex128
num := byte('a')        // byte (uint8)

str := "String"
str := `Multiline
string`
```
Built-in types are:
- `string`
- `bool`
- `int8`, `uint8` (`byte`), `int16`, `uint16`, `int32` (`rune`), `uint32`,
  `int64`, `uint64`, `int`, `uint`, `uintptr`
- `float32`, `float64`
- `complex64`, `complex128`

<!--
### Arrays and Slices

### Maps

### Structs

### Interfaces

### Functions

### Packages
Only names starting with uppercase are exported outside the package.

## Standard Library

## Compiling Windows
- Download https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/sjlj/x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z
- Extract to C:\Devel\mingw64
- Add C:\Devel\mingw64\bin and C:\Devel\mingw64\x86_64-w64-mingw32\bin to PATH
-->
