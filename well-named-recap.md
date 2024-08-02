# Modular well-named recap

## Naming

[Intuitive file names](https://github.com/code-craft-igt-1/well-named-in-cpp-arundas005) indicate Single Responsibility = "one reason for change".
BTW, what work can [gtest take](https://github.com/code-craft-igt-1/well-named-in-cpp-SherawatHari) in this?

[Retaining naming and meaning](https://github.com/code-craft-igt-1/well-named-in-cpp-AviB183/blob/1440afe6345a694851e57286461a9733618417a7/ColorConstants.h) to track the maximum color number

Avoid generic names. Generic names often have `Utils` and `Manager` in them. [Example specific naming](https://github.com/code-craft-igt-1/well-named-in-cpp-vivekantonyo)

## Encapsulation vs Separation

[Here is an intuitive file-naming](https://github.com/code-craft-igt-1/well-named-in-cpp-surdhawal20), which keeps together all color-pair functionality. 

[Keep related code in same namespace](https://github.com/code-craft-igt-1/well-named-in-cpp-pavanshenoy89/blob/5aa8f292c6f22eb8c04ee844e9028fc4199835fd/colorcoder.h)

[Specific file names](https://github.com/code-craft-igt-1/well-named-in-cpp-Sasikalaas28) force you to make small files.

Trade-offs:

- Keeping things together means we modify things in one place - but developers can step on each others toes
- Keeping `ColorPair` with data and a `Utils` file with conversion and printing feels like we separated, but a single functionality-change may now be spread across files

What's the best way? Explore in the next assignment :)

## Splitting files

[Compiler and linker](https://github.com/code-craft-igt-1/well-named-in-cpp-arundas005/blob/c49c48622dcd5447f181bfaeeee6b028bc22849c/CMakePresets.json)

**Splitting patterns**:

1. Split test code from production code
1. New functionality in its own file

## Comments

It's hard to keep comments in sync with functionality. Write _why_ the code is written, not what it does.

```cpp
 // Class to represent a color pair
 class ColorPair {
 private:
     MajorColor majorColor;
     MinorColor minorColor;
 public:
     ColorPair(MajorColor major, MinorColor minor);
     ...
     static int GetNumberOfMajorColors();
```

## Testability

Easy to test: `int GetPairNumberFromColor(...`

Hard to test: `void PrintReferenceManual()`

[Asserts for printing](https://github.com/code-craft-igt-1/well-named-in-cpp-shivraj0058/blob/f3be90cbe183fb729d4305f9c7b287f35e32a8d4/TestColorPair.cpp), to reduce manual test effort.

[Test against reference output](https://github.com/code-craft-igt-1/well-named-in-cpp-arundas005/blob/master/RefManual.txt)

Are these tests very [sensitive](https://github.com/code-craft-igt-1/well-named-in-cpp-arundas005/actions/runs/10197155234/job/28209402109)? Do they pay back the effort?

Splitting the responsibility inside the print function enables [asserting the value](https://github.com/code-craft-igt-1/well-named-in-py-manojsubrahmanian/blob/bac265e7911e1c3d9d1e7bb32c749593aeb6591d/refmanualtest.py) before printing it. See the [same in cpp](https://github.com/code-craft-igt-1/well-named-in-cpp-manojsubrahmanian/blob/631bed0bd3d58d7a3225e81244296b404ea0f5f7/ColorCodingFormatter.cpp)

>Can we assert the user need?
