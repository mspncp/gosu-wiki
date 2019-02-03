# Basic Concepts

## Options Hash
Hashes are special parameters that you can pass in as options into some methods in Gosu. They are found in the documentation as `options = {}`. A default hash value is always set for each option. To use a hash simply put the name of the option, followed by a colon then assign the new value.
* For example in the [Image.from_text method](https://www.rubydoc.info/github/gosu/gosu/master/Gosu%2FImage%2Efrom_text) `.from_text(text, line_height, options = {})` the option hash to bold text is given as `:bold (bool) — default: false `. This can be passed in with `bold: true`.

This method then becomes `.from_text("This text will be bold", 12,{bold: true})`.

You can see more examples of Options hash in the topics below.

## Z Ordering

All drawing operations in Gosu accept a floating-point value called "z". Things drawn with a higher z position will be drawn on top of those with a lower z position. If two things have the same z position, they will be drawn in the order the drawing functions have been called.

## Tileability

Functions related to image creation accept a boolean "tileable" argument that controls how the edges of images behave when the image is resized or rotated. Try to notice the subtle difference between these two images, drawn with `scale_x = scale_y = 10.0`:

[[hard_borders.png|alt=Effect of the tileable parameter]]

When you scale or rotate an image, or draw an image at a non-integer position like `10.5`, your GPU will *interpolate* the image contents to fill the rectangle.

The left image was created with `tileable: false` (the default), and the borders fade out. The right image, which was created with `tileable: true`, has sharp borders.

As a rule of thumb, map tiles should be created with `tileable` set to `true` to avoid tiny gaps between tiles, and everything else should use the default value.

Note that images created with `retro: true` (or `IF_RETRO` in C++) are never interpolated, and are not affected by "tileability."

## Order of Corners

In functions that expect arguments (coordinates or colours) for the four corners of a rectangle, you can either pass parameters clockwise or in a Z shape:

[[corner_indices.png|alt=Order of corners in Gosu]]

Gosu understands both, so use what you find more natural.

## Drawing with Colours

Almost all image drawing functions accept modulation colours. The colours of all pixels on the source image will be *multiplied* with these colours. If you draw a red image (RGB 200, 0, 0) with a gray modulation colour (RGB 128, 128, 128), the result will be (RGB (200 * 128) / 255 = 100, 0, 0). Colour parameters can be used only to *reduce* the intensity of colours in an image, they cannot amplify them.

The most common way to use colour parameters is to use white with an alpha value less than 255, for example, (RGBA 255, 255, 255, 128). This will draw an image at 50% opacity. But can also use colour parameters to darken images or to draw them in a different hue, which works best with gray scale images.