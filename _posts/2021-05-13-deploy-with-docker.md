```bash
docker load -i image.tar

docker run -it \
  -p 8000:3000 \
  --mount type=bind, source=/canon,target=/canon \
  image.tar
```

