# Inspection

- [How to see container content](#how-to-see-container-content)

## How to see container content

If the image contains a shell, you can run an interactive shell container
using that image and explore whatever content that image has. If `sh` is
not available, the busybox `ash` shell might be.

```sh
docker run -it <image name> sh
```

Or for images with an entrypoint:

```sh
docker run -it --entrypoint sh <image name>
```

Or if you want to see how the image was built, meaning the steps in its
`Dockerfile`, you can:

```sh
docker image history --no-trunc <image name> > image-history.txt
```

The steps will be logged into the `image-history.txt` file.

Source: [SO](https://stackoverflow.com/questions/44769315/how-to-see-docker-image-contents).
