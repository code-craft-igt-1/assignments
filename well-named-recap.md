# Modular well-named recap

## Naming

[Intuitive file names](https://github.com/code-craft-igt-1/well-named-in-cpp-arundas005) indicate Single Responsibility = "one reason for change".
BTW, what responsibility does gtest take away in this?

[Retaining naming and meaning](https://github.com/code-craft-igt-1/well-named-in-cpp-AviB183/blob/1440afe6345a694851e57286461a9733618417a7/ColorConstants.h) to track the maximum color number

Avoid generic names. Generic names often have `Utils` and `Manager` in them. [Example specific naming](https://github.com/code-craft-igt-1/well-named-in-cpp-vivekantonyo)

## Encapsulation vs Separation

[Here is an intuitive file-naming](https://github.com/code-craft-igt-1/well-named-in-cpp-surdhawal20), which keeps together all color-pair functionality. 

[Specific file names](https://github.com/code-craft-igt-1/well-named-in-cpp-Sasikalaas28) force you to make small files.

Trade-offs:

- Keeping things together means we modify things in one place - but developers can step on each others toes
- Keeping `ColorPair` with data and a `Utils` file with conversion and printing feels like we separated, but a single functionality-change may now be spread across files

What's the best way? Explore in the next assignment :)

## Splitting files

[Compiler and linker](https://github.com/code-craft-igt-1/well-named-in-cpp-arundas005/blob/c49c48622dcd5447f181bfaeeee6b028bc22849c/CMakePresets.json)

## Splitting patterns:

1. Split test code from production code
1. New functionality in its own file

## Testability

Easy to test: `int GetPairNumberFromColor(...`

Hard to test: `void PrintReferenceManual()`

> Can you think of asserts for printing, to reduce the manual test effort?
