# How to build a Docker image

The simplest build. **Note:** there is no tagging.
```
docker build .
```

With tagging:
```
# Example 1:
docker build -t yourusername/repository-name .
# Example 2:
docker build --tag python-docker .
```

Docker listing the dockers:
```
docker 
```