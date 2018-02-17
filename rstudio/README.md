# RStudio *contained*

If the latest versions of [RStudio](https://www.rstudio.com/) for Linux don't support your computing environment's operating system version, you can avail yourself of Singularity and still use it!
This container provides a complete R and RStudio environment.

## Usage

```
$ singularity shell shub://NIH-HPC/singularity-examples:rstudio
Singularity rstudio.simg:~> rstudio
```

And that's it!
If you have a graphical connection, you should see RStudio warmly greeting you.

## Customization

You can of course edit the definition file and build the container anew, or [use the container on singularity hub as a base image](http://singularity.lbl.gov/build-shub), or prepare it from a local sandbox.
In all cases, we advise building/installing all R packages inside the container to ensure binary compatibility.

Below, the sandbox preparation is described.
It's likely to be the most appropriate for this use case since you're not looking to freeze the contents of the container, as would be the case in the default image format.
It's useful in order to be able to update the software and add a few more R packages over time without having to re-bootstrap the container each time.

```
$ sudo singularity build --sandbox rstudio shub://NIH-HPC/singularity-examples:rstudio
$ sudo singularity shell --writable rstudio
Singularity rstudio:~> apt-get update && apt-get -y upgrade && apt-get clean
Singularity rstudio:~> # make your other desired changes now
Singularity rstudio:~> exit
$ # convert the sandbox image to squashfs
$ sudo singularity build rstudio.simg rstudio
$ # copy it to the system you want to run it on
$ scp rstudio.simg biowulf:/data/username/
```
