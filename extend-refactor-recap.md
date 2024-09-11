# Recap of extensions

## Data structures to store messages

[Mapping enums](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-manojsubrahmanian/blob/4608a4b1a075490f65140a06ffda5989e90b6a32/vitals_messages.h)

[Mapping strings](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-Lokesh-Kumar-121/blob/ef5f17a648f3fbb7a3ce6390970fcce0f5600b0b/monitor.cpp)

## Common comment

In most repos, the strings aren't automatically tested.
Also, it's hard to test all the situations in all the languages manually each time.
Of course, the "understand-ability" of the translation can only be confirmed manually by native speakers.
But other things can go wrong, like missing a translation in a particular language, etc.

>Can you think of any asserts to safeguard against that?

## Thresholds

[Declarative code to express requirements](https://github.com/code-craft-igt-1/simple-monitor-in-cpp-manojsubrahmanian/blob/4608a4b1a075490f65140a06ffda5989e90b6a32/vitals_monitor.h)

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
