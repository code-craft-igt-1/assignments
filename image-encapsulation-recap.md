# Image encapsulation recap

## Semantics of `shared_ptr`

[Use of a shared pointer](https://github.com/code-craft-igt-1/image-encapsulation-pavanshenoy89/blob/3ff11a7d80753eda0ff5beb8f3949d44ec406de8/image-encapsulate.cpp) means both `main()` and `ImageBrightener` share the image.

It also means you can brighten an image twice. Did you intend to allow that?

## Passing by reference - a smell? 

Passing parameters by reference can signal an [opportunity for encapsulation](https://github.com/code-craft-igt-1/image-encapsulation-pavanshenoy89/pull/1/files/0ac4e0d7e5192c1455de55164119e02beeaa88c9..3ff11a7d80753eda0ff5beb8f3949d44ec406de8#diff-e1913707a50bb5fb0a280f8d5d9eefd2cd582843b1c854a675b74fea300030f8).

>Whenever you pass a variable by reference, ask its purpose - does it fit in another class?

## Reduction in complexity

Treat 2D pixels as single-dimension

```cpp
for (int x = 0; x < m_inputImage->m_rows; x++) {
        for (int y = 0; y < m_inputImage->m_columns; y++) {
```
[becomes](https://github.com/code-craft-igt-1/image-encapsulation-SivarajAyyavoo/blob/47e8606861d0257ed645d2b580de8b62bb658fc1/brightener.cpp)
```cpp
for (int imageArrayIndex = 0;
        imageArrayIndex < (m_inputImage->m_columns * m_inputImage->m_rows); imageArrayIndex++) {
```

---

You can also [separate the processing](https://github.com/code-craft-igt-1/image-encapsulation-pra1788/blob/2fb94e6b0659d782468c3afbdda19fc0290d2743/ImageBrightener.h#L12) from the iteration

```cpp
for (int x = 0; x < m_inputImage->GetRows(); ++x) {
    for (int y = 0; y < m_inputImage->GetColumns(); ++y) {
        attenuatedPixelCount += ProcessPixel(x, y);
    }
}
```

---

Separation of [attentuation-counting](https://github.com/code-craft-igt-1/image-encapsulation-pravocodes/blob/475a13ac1eb532b5c5fb66b78818a180bb8b7ed8/brightener.cpp#L15) from the actual brightening. This will be useful when we want to avoid brightening the image when too much attenuation would occur.

```cpp
void ProcessPixel(const std::shared_ptr<Image>& image,
    int x, int y, int addValue, int attenuatedPixelCount) {
    int pixelValue = image->GetPixel(x, y);
    if (IsPixelAttenuated(pixelValue, addValue)) {
        ++attenuatedPixelCount;
    }
    int newPixelValue = GetBrightenedPixelValue(pixelValue, addValue);
    image->SetPixel(x, y, newPixelValue);
}
```
