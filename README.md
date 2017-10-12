# sara-server-vre
Virtual Research Environment for Sara Server - container build scripts


## Use prebuild image
```
   cd /tmp
   singularity pull --name "sara-server-vre.img" shub://c1t4r/sara-server-vre
   ./sara-server-vre.img
```

## Build local image

```
cd /tmp
singularity create -s 2048 sara-server-vre.img
singularity bootstrap sara-server-vre.img ./Singularity
./sara-server-vre.img
```
