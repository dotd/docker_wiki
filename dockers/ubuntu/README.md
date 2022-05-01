In this example we shw how to build a docker and have a python 
with numpy installed on it.

Building the docker:
```buildoutcfg
docker build --tag python-docker .
```

Now, running in interactive mode:
```buildoutcfg
docker run -it python-docker bash
```

Inside the interactive mode we can do:
```buildoutcfg
 docker run -it python-docker bash
```

