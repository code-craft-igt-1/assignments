# Passing an image: Recap

Local variables are placed on stack. When large objects (like images) are placed on stack, it can overflow. They can be placed on the heap using allocation operators like `new` or `malloc`.

## Allocating the image on the heap

```cpp
    Image* image = new Image;
    image->rows = 512;
    image->columns = 512;
	std::cout << "Brightening a 512 x 512 image\n";
    ImageBrightener brightener(*image);
```

>Solves the issue. However, the code needs to be aware of the size of the Image object, and manage its lifetime. Where do we free the allocated memory?

## Use unique_ptr to handle memory "automatically"

[Pixel logic and heap](https://github.com/code-craft-igt-1/pass-an-image-pavanshenoy89/blob/edbf325c46c5186c45ac5588f594d98feda6dbe2/image.h) in the `Image` class

[Make unique ptr to pixel data on the heap](https://github.com/code-craft-igt-1/pass-an-image-pra1788/blob/8e3971940a7f5d21bd10f2b1e088e1db4c467552/brightener.h) and [define "move" constructor](https://github.com/code-craft-igt-1/pass-an-image-pra1788/blob/8e3971940a7f5d21bd10f2b1e088e1db4c467552/brightener.cpp).

## Use unique_ptr to hand-over

[Hand-over ownership](https://github.com/code-craft-igt-1/pass-an-image-surdhawal20/blob/daf2d954781d0cd1d2ebdf830bbccbf2538cc088/pass-an-image.cpp) to the brightener.

## Other unique approaches

Attenuated pixel count [as a data member](https://github.com/code-craft-igt-1/pass-an-image-shunmugasundaramp/blob/78f78e0dbc0a8278094cca90cc4b37c36ec01420/Brightener.h) instead of a return value - what is its lifetime?

Testing the brightener [using random pixel values](https://github.com/code-craft-igt-1/pass-an-image-J-Suriya/blob/b2a2d637dd77ecc9fc20c8cc8f094cf0c72003be/pass-an-image.cpp) in a distribution

[cmake in a windows runner](https://github.com/code-craft-igt-1/pass-an-image-manojsubrahmanian/blob/10dbcbe5a0bfd380a941562c597cfc120ffba437/.github/workflows/msbuild2019.yml)

## Pitfalls

Returning private pointer complicates object lifetimes and ownership. It's hard to judge how long the caller of this function will keep the returned pointer. So when to free the pixels?

```cpp
uint8_t* Image::getPixelValues() {
	return m_pixels;
}
```

---

Reference data members also make lifetimes tricky.

```cpp
class ImageBrightener {
 private:
	Image& m_inputImage;
 public:
    ...
}
```

The instantiator of `ImageBrightener` must ensure that the `Image` object lasts longer than the `ImageBrightener` object.
