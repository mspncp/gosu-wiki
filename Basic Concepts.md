# Basic Concepts

[ ![Please post feedback and additions as comments to this page and visit the boards for questions outside the scope of a single wiki page. Thank you!](board_link.png) ][boards]

## Z Ordering

All drawing operations in Gosu accept a floating-point value called "z" (technically, a `double`). Things drawn with a higher z position will be drawn over those with a lower one. If two things have the same z position, they will be drawn in the order the drawing functions were called.

If you do not wish to use z ordering, just pass the same constant all the time.

## Tileability

Functions related to image creation accept a boolean "tileable" argument. This is a consequence of using 3D hardware acceleration. Try to notice the subtle difference between these two, overstretched images:

[[hard_borders.png|alt=Effect of the tileable parameter]]

When you draw an image with stretching factors other than 1.0 (10.0 in this case) or at odd coordinates, it will become interpolated—which, in general, is much better than getting all pixel-y.

But take a look at the image's borders. The image of the left girl was created with tileable set to `false` (the default) and the borders fade out. The image of the right girl, which was created with tileable set to 'true, does not fade out at all, but just ends on its borders.

While most images should not be tileable, you should always pass true for map tiles.

## Order of Corners

In all functions that expect arguments for all four corners of a rectangle or quadrilateral, except `ImageData::draw` (in C++), you can either pass clockwise coordinates, or coordinates in the following order (a Z shape):

[[corner_indices.png|alt=Order of corners in Gosu]]

## Drawing with Colours

Almost all image drawing functions accept modulation colours. The colours of all pixels on the source image will be multiplied with these colours, where a channel value of 255 corresponds to the maximum value of 1.0. This means modulation colours can be used only to reduce particular channels of an image.

The most obvious use of this is to supply a colour with an alpha value less than 255 so the image will drawn transparently, but you can also use this to darken images or to draw them in a different hue (which works best if the original image is mostly grayscale).

[boards]: http://www.libgosu.org/cgi-bin/mwf/forum.pl "Gosu Boards"
