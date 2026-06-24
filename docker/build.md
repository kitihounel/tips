# Docker build tips

- [Export an image as a tar archive](#export-image-as-a-tar-archive)

## Export an image as a tar archive

```sh
docker build -t $MY_IMAGE_TAG -o type=docker,dest=$OUTPUT_IMAGE_ARCHIVE .
```

Later, you can load the image and run it:

```sh
docker image load -i $OUTPUT_IMAGE_ARCHIVE
docker run $MY_IMAGE_TAG
```
