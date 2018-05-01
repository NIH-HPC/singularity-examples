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

Note that the second definition file hardcodes the `torch.simg` image name. Note also that
no effort was made to install well defined versions of the different tools. For a production
container it might be good to fix versions.

