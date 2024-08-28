# Passing tests recap

[Naming](https://github.com/code-craft-igt-1/test-failer-in-cpp-manojsubrahmanian/blob/cd780506c5e46f628ae6184681108fab860290c5/TShirtSizeCalculator.cpp) of constants

## Attention to detail

[Step names](https://github.com/code-craft-igt-1/test-failer-in-cpp-shivraj0058/blob/835b9ac7c1d30158b2ae0360c9f9359b90478a5c/.github/workflows/main-workflow.yml)

[All is well](https://github.com/code-craft-igt-1/test-failer-in-cpp-SherawatHari/blob/43da242ea525bee9bfdd1b2a977eb6ea5fd9020e/weatherreport.cpp)

## Replicating implementation in test

Disadvantage: May miss out on single responsibility

```cpp
std::string expectedColorMap = 
        "  No.        Major Color        Minor Color\n"
        "----------------------------------------------\n"
        "    1    |          White    |           Blue\n"
        "    2    |          White    |         Orange\n"
        "    3    |          White    |          Green\n"
```

Alternative: Instead of testing the equality of the whole output, test each aspect of the user's expectation separately:
- clear heading
- formatting of one row has aligned separators (can sample two rows with short and long color names)
- 25 rows
- content of the rows

Advantage: By forcing each test to be independent, you force yourself to write separate functions to print header, format one row, make sequence of rows, etc.

