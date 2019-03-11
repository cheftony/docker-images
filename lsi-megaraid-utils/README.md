# lsi-megaraid-utils
Docker container for running MegaCLI and StorCLI

## Running the container

```bash
docker run --rm -ti --privileged cheftony/lsi-megaraid-utils
```

> Note that the `--rm` will delete the container for you when you exit it, and
> `privileged` mode is required so the container can talk directly to the hardware.