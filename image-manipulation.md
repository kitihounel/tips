# Tips for image editing

- [Make image background transparent](#make-image-background-transparent)

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
