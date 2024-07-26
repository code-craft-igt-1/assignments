# Recap of starter assignment

## Why 0.001?

The test code: why is `epsilon` 0.001?

```cpp
float epsilon = 0.001;
EXPECT_LT(std::abs(computedStats.average - 4.525), epsilon);
```

```python
epsilon = 0.001
self.assertAlmostEqual(computedStats["avg"], 4.525, delta=epsilon)
```

## Test to pass

Does this test check if the reult is `nan`?

```cpp
EXPECT_EQ(std::isnan(computedStats.average),0);
EXPECT_EQ(std::isnan(computedStats.max),0);
EXPECT_EQ(std::isnan(computedStats.min),0);
```

## State of `Stats`

```cpp
Stats stats;
// ** Stats is uninitialized here **
if (numbers.empty()) {
    stats.min = std::numeric_limits<float>::quiet_NaN();
    stats.max = std::numeric_limits<float>::quiet_NaN();
    stats.average = std::numeric_limits<float>::quiet_NaN();
    return stats;
}
```

## Treating warnings as errors

In [CMakeLists.txt](https://github.com/code-craft-igt-1/spring-in-cpp-junaijm/blob/c50ad5abd6820f8e6b5c1d286e68bca418f1d93c/CMakeLists.txt)

`set(CMAKE_COMPILE_WARNING_AS_ERROR ON)`

## Use of templates

Enabling any 'type' that has `+=`, `<` and `>`

```cpp
template<typename T>
Stats Statistics::ComputeStatistics(const std::vector<T>& dataset) {
```
