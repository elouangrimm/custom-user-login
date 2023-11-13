# The image data image format

> Introducing the brand new image data image format!

Image data (pronounced 'image data') is a new lossless image format. It stands for "image data not pngs". 

## Structure

Image data is a subset of json. It's just a javascript object with the following properties.

### `width`

How many pixels wide the image is.

### `height`

How many pixels high the image is.

### `data`

An array of numbers containing information about the colour of each pixel. Pixels are listed in row-order and then column-order. For example, a 3 by 2 image would be laid out like this:

| 0 | 1 | 3 |
|---|---|---|
| 4 | 5 | 6 |

Each pixel is represented by a list of four numbers in the array, in the following order

- red
- green
- blue
- alpha (opacity)

All numbers are between 0 and 255 (inclusive).

## Weaknesses

- Image data's compression algorithm is terrible. In comparison testing, it performed worse than PNG, WEBP, JPEG, and GIF, in nearly all cases.

- It's not well-supported by old browsers like chrome and arc. Please make sure to upgrade to a modern browser to use the brand new image data image format.

## Strengths

- It has the simplest and most entertaining specification. (Believe me, I read them all).

- It's easy to implement on any machine.

- It does have *some* old-browser support, such as the `putImageData` and `getImageData` functions.

- The lack of compression is inconsequential when using a slippy mindset. You'll save loads of space and bandwidth by staying simple elsewhere.

- It's counter-culture and satirical.

- [Minification is evil](/wikiblogarden/better-computing/worse-computing/minification).

## How to use image data in your website

Coming soon. Follow the [feed](/feed) for more.

<br>

Back to the [wikiblogarden](/wikiblogarden).
