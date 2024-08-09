# Recap of tests

## Alignment

[Separating](https://github.com/code-craft-igt-1/test-failer-in-cpp-akheelassadi/blob/ec6a7c7beeebd3d6734646071ae71c8260756bd4/misaligned.cpp) the generation from the formatting + output

The problem of repeating the implementation in the test - double work to change?

```cpp
std::vector<std::string> expected_output = {
    "Index=0, MajorColor=White, MinorColor=Blue",
    "Index=1, MajorColor=White, MinorColor=Orange",
    "Index=2, MajorColor=White, MinorColor=Green",
    "Index=3, MajorColor=White, MinorColor=Brown",
    ...
}
```

or

```cpp
std::string expectedColorMap = 
        "  No.        Major Color        Minor Color\n"
        "----------------------------------------------\n"
        "    1    |          White    |           Blue\n"
        "    2    |          White    |         Orange\n"
```

or

```cpp
std::string generateExpectedOutput(const ColorMap& colorMap) {
    ...
    for (size_t i = 1; i < colorPairs.size(); ++i) {
        colorPairStream << i << " | "
            << colorPairs[i].second << " | "
            << colorPairs[i].first << '\n';
    }
```

Specify [the property of alignment](https://github.com/code-craft-igt-1/test-failer-in-cpp-AviB183/blob/1ebcf23723747d570f9749973a023349f0238822/misaligned.cpp)

## Tshirt size

Is 38 `M` or `S`?

Maybe in this code, 38 to 42 looks to be Medium?

```cpp
    if (cms < 38) {
        sizeName = 'S';
    } else if (cms > 38 && cms < 42) {
        sizeName = 'M';
    }
```

But what about the user's experience?
