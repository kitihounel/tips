# Tips for image editing

- [Make image background transparent](#make-image-background-transparent)
- [Resize an image](#resize-an-image)
- [Get image info]

## Make image background transparent

Using `ImageMagick` (here we have a white bg, but you can specify any color):

```bash
convert input-image.png -transparent white transparent.png
```

One can also use hex color codes for the same result:

```bash
convert input-image.png -transparent '#ffffff' transparent.png
```

**Important:** This does not work on JPEG images since JPEG does not support transparent background.

Source: [SO](https://stackoverflow.com/a/11115408).

## Resize an image

```bash
convert input.jpg -resize 800x output.jpg     # Resize to a specific width while maintaining aspect ratio
convert input.jpg -resize 800x600 output.jpg  # Resize to fit within a maximum width and height (e.g., within a 800x600 pixel box)
convert input.jpg -resize 50% output.jpg      # Resize in a given proportion
mogrify -resize 50% image.jpg                 # Resize in place
```

## Get image info

```bash
identify image.png
identify -verbose image.jpeg
```
