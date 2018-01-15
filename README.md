# sara-server-vre
Virtual Research Environment for Sara Server - container build scripts

This is the VRE main spec containing a Java Runtime Environment plus Eclipse
used for the development of the SARA service.
A local postgres database is integrated, too. The source is a docker repo
which is being pulled on build time and used to locally run a postgresql
server using udocker.
This VRE has no external requirements whatsoever once the image has been built.

## Use prebuild image
```
   cd /tmp
   singularity pull --name "sara-server-vre.img" shub://c1t4r/sara-server-vre
   ./sara-server-vre.img
```

## Build local image (Singularity 2.3)

```
cd /tmp
singularity create -s 2048 sara-server-vre.img
singularity bootstrap sara-server-vre.img ./Singularity
./sara-server-vre.img
```

## Build local image (Singularity 2.4)

```
TODO
```
