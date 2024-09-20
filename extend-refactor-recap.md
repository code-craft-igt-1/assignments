# Recap of extensions

## Data structures to store messages

[Mapping enums](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-manojsubrahmanian/blob/4608a4b1a075490f65140a06ffda5989e90b6a32/vitals_messages.h)

[Mapping strings](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-Lokesh-Kumar-121/blob/ef5f17a648f3fbb7a3ce6390970fcce0f5600b0b/monitor.cpp)

[UTF-8 messages](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-Sasikalaas28/blob/733e8a7269b98bd80fd1a5964f1d1962c0026586/monitor.cpp)

[Use of `boost` library](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-lll2yu/blob/4c568883ecfbcde78a816fe6596d3fe74d6ae334/vitalchecker.cpp) to offload standard functionality to an off-the-shelf library.

## Common comment

In most repos, the message strings aren't automatically tested.
Also, it's hard to test all the situations in all the languages manually each time.
Of course, the "understand-ability" of the translation can only be confirmed manually by native speakers.
But other things can go wrong, like missing a translation in a particular language, etc.

>Can you think of any asserts to safeguard against that?

[Parametrized tests](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-lll2yu/blob/4c568883ecfbcde78a816fe6596d3fe74d6ae334/test-vitalchecker.cpp) are one way to reduce duplication in repeating tests with different data.

## Thresholds

[Declarative code to express requirements](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-manojsubrahmanian/blob/4608a4b1a075490f65140a06ffda5989e90b6a32/vitals_monitor.h)

[Declarative ranges](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-arundas005/blob/b3fbdcd424af36bd8a34e7b1140e8382b03ae4c8/monitor.cpp) using `VITAL_RANGE_CLASSIFICATION`

## Remove generic naming for Single Responsibility

The word `check` is generic and doesn't say the purpose of checking, or what's being checked.

Try renaming this function without using the word `check`

```cpp
bool checkAndDisplay(float value, float lowerLimit, float upperLimit,
    const std::string& messageBelow, const std::string& messageAbove) {

    bool result = true;
// These functions check against the limits AND also perform the display of the given message
    result &= !isBelowLowerLimit(value, lowerLimit, messageBelow);
    result &= !isApproachingLimit(value, lowerLimit, tolerance, messageBelow);
    result &= !isExcedingLimit(value, upperLimit, tolerance, messageAbove);
    result &= !isAboveUpperLimit(value, upperLimit, messageAbove);
    return result;
}
```
