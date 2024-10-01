# action-docker-build-push

> Setup docker, build image and push

## Usage

```yml
      - name: Docker build push
        uses: seepine/action-docker-build-push@v1
        with:
          registry: docker.io
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
          platforms: linux/amd64,linux/arm64
          tags: |
            docker.io/${{ secrets.DOCKER_USERNAME }}/demo:latest
            docker.io/${{ secrets.DOCKER_USERNAME }}/demo:1.2.3
```

## Set dockerfile

```yml
      - name: Docker build push
        uses: seepine/action-docker-build-push@v1
        with:
          registry: docker.io
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
          context: .                # default .
          file: ./build/Dockerfile  # default Dockerfile
          platforms: linux/amd64,linux/arm64
          tags: |
            docker.io/${{ secrets.DOCKER_USERNAME }}/demo:latest
            docker.io/${{ secrets.DOCKER_USERNAME }}/demo:1.2.3
```

## Set proxy


```yml

# Set into act runner config.yml also
env:
  HTTP_PROXY: http://192.168.2.4:7890/
  HTTPS_PROXY: http://192.168.2.4:7890/
  NO_PROXY: 127.0.0.1,localhost,172.17.0.1

jobs:
  build-image:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 1

      - name: Docker build push
        uses: seepine/action-docker-build-push@v1
        with:
          registry: docker.io
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
          platforms: linux/amd64,linux/arm64
          tags: |
            docker.io/${{ secrets.DOCKER_USERNAME }}/demo:latest
            docker.io/${{ secrets.DOCKER_USERNAME }}/demo:1.2.3
```
