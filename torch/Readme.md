2 step torch container example
==============================

In this example, a final container is built by first generating a base image
and then adding extras to the base image. This was done b/c building the base
image takes a long time and extras are more likely to get changed/updated. That
allows quicker iteration on the second part of the build.

Build the first stage container:

```
$ sudo singularity build torch.simg Singularity.torch
```

Then extend that container with the extra tools/rocks:

```
$ sudo singularity build torch-extras.simg Singularity.torch-extras
```

Note that the second definition file hardcodes the `torch.simg` image name.
Note also that no effort was made to install well defined versions of the
different tools. For a production container it might be good to fix versions.


This is a GPU based container. Usage:
```
$ singularity shell --nv -B $PWD:/mnt/work --pwd /mnt/work torch-extras.simg
(singularity)$ th

  ______             __   |  Torch7
 /_  __/__  ________/ /   |  Scientific computing for Lua.
  / / / _ \/ __/ __/ _ \  |  Type ? for help
 /_/  \___/_/  \__/_//_/  |  https://github.com/torch
                          |  http://torch.ch

th> a = torch.rand(5,3)

th> print(a)
 0.7383  0.2488  0.5722
 0.4096  0.4259  0.0669
 0.4246  0.9077  0.4638
 0.2936  0.9162  0.8862
 0.0095  0.6689  0.8819
[torch.DoubleTensor of size 5x3]
```


