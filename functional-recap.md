# Recap of reducing complexity

## Low semantic distance

Which reads better?

```cpp
bool checkVitals(..)

if (checkVitals(..)) {...}
```

---

```cpp
bool vitalsAreInRange(..)

if (vitalsAreInRange(..)) {...}
```

## The struggle to limit complexity

```cpp
if (isTempCritical | isPulseOutOfRange | isSpo2OutOfRange) {
  cout << "One of the vital (Temperature/Pulse/Spo2 is out of range !\n";
  return false;
}
```

```cpp
return temperatureInRange && pulseInRange && spo2InRange;
```

---

Suggestions:

[Use a loop instead of a conjunction](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-surdhawal20/blob/41798474a72ea48819c8b11907612e054ceb88d8/monitor.cpp)

[Reduced complexity](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-arundas005/blob/fdd1c8cb3eb0eabecd7c9c250bc9f63d8b3bd911/monitor.cpp) = [Fewer tests for full coverage](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-arundas005/blob/fdd1c8cb3eb0eabecd7c9c250bc9f63d8b3bd911/test-monitor.cpp)

[Use any_of](https://en.cppreference.com/w/cpp/algorithm/all_any_none_of)

## Repeating patterns

Is there any disadvantage of repeating the range check for every parameter?

```cpp
bool isTemperatureCritical(float temperature) {
  return (temperature > 102 || temperature < 95);
}

bool isPulseRateCritical(float pulseRate) {
  return (pulseRate < 60 || pulseRate > 100);
}

bool isSpo2Critical(float spo2) {
  return (spo2 < 90);
}
```

## Testing ranges

[Testing by the "property" of range-inclusion](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-manojsubrahmanian/blob/12f7ed9f40c0935a9305f306e2c21c2ac4795e1a/test-monitor.cpp)

[Easy-to-read boundary checks](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-shunmugasundaramp/blob/cae96a498bd90315e91f55df995f99b01aadbdab/test-monitor.cpp)

---

SPO2 cannot go beyond 100% saturation. Does this test case make sense?

```cpp
EXPECT_FALSE(areVitalsNormal(98.6, 75, SPO2_UPPER_LIMIT + 0.1));
```

## Mocking dependencies

[Speed up and inject dependency](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-lll2yu/blob/f608e6a2194fae6007f0f80804d0980a210d5cc5/test-vitalchecker.cpp)

## Organizing files

[Split for single responsibility](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-pravocodes/pull/1/files) of displaying the message
