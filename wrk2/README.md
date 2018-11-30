# wrk2

Docker image for wrk2 using Alpine

# How to

```bash
docker run --rm --net=host cheftony/wrk2 wrk -t4 -c200 -d10s -R2000 --latency http://localhost
```
