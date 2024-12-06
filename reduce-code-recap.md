# Reduce code - Recap

Have a look at the `README.md` in your repository. **Part 1** is about having a method called `processPixels` in the `Image` class. It needs to have the iteration (for loops) in it.

```cpp
void processPixels() {
    for (int x = 0; x < m_rows; x++) {
        for (int y = 0; y < m_columns; y++) {
            // if we put all the processing here, this class will become
            // a big ball of mud!
        }
    }
}
```

So we 'inject' the processing into the iteration

```cpp
class IPixelProcessor {
 public:
    virtual uint8_t processPixel(uint8_t pixelValue, int& attenuationCount) = 0;
};

void processPixels(IPixelProcessor& pixelProcessor) {
    for (int x = 0; x < m_rows; x++) {
        for (int y = 0; y < m_columns; y++) {
            int pixelIndex = x * m_columns + y;
            m_pixels[pixelIndex] = pixelProcessor.processPixel(m_pixels[pixelIndex], m_attenuationCount);
        }
    }
}
```

Now start with the pixel processor that brightens the whole image. Notice that it's a class with just one function. We could have made it a plain function, but we need to inject the pixel processor, hence the class derives from `IPixelProcessor`

```cpp
class FixedBrightener : public IPixelProcessor {
 public:
    virtual uint8_t processPixel(uint8_t pixelValue, int& attenuatedCount) {
        if (pixelValue > (255 - 25)) {
            ++attenuatedCount;
            return 255;
        } else {
            return 25;
        }
    }
};
```

...and remove the corresponding iteration from ImageBrightener

```cpp
int ImageBrightener::BrightenWholeImage() {
    FixedBrightener fixedBrightener;
    m_inputImage->processPixels(fixedBrightener);
    return m_inputImage->m_attenuatedCount;
}
```

Now we can make an brightening-image-adder as well. But it needs the x and y coordinates.
So we add them to the base class, then the derived class...

What does it look like with lambdas? Are these changes easier to make?

The `processPixels` function now looks like this:

```cpp
void processPixels(std::function<uint8_t(uint8_t, int, int)> processAPixel) {
    for (int x = 0; x < m_rows; x++) {
        for (int y = 0; y < m_columns; y++) {
            int pixelIndex = x * m_columns + y;
            m_pixels[pixelIndex] = processAPixel(m_pixels[pixelIndex], x, y);
        }
    }
}
```

...and `BrightenWholeImage` can capture `attenuatedCount` in a lambda, so we don't need to make it a member of `Image`

```cpp
int ImageBrightener::BrightenWholeImage() {
    int attenuatedCount = 0;
    m_inputImage->processPixels([&attenuatedCount](uint8_t pixelValue, int, int) {
        if (pixelValue > (255 - 25)) {
            ++attenuatedCount;
            return 255;
        } else {
            return pixelValue + 25;
        }
    });
    return attenuatedCount;
}
```
