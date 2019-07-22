# Singularity image of [aCNViewer](https://github.com/FJD-CEPH/aCNViewer)

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/3290)

The [docker image](https://hub.docker.com/r/fjdceph/acnviewer/) of [aCNViewer](https://github.com/FJD-CEPH/aCNViewer) is not working with Singularity without `sudo` because several files have read/execute permissions only for the file owner (root). This repository hosts a very simple [Singularity definition file](Singularity) that bootstraps the docker image and assigns the same permissions of the file owner (`u`) to the `other` group (`o`) for the folder containing aCNViewer scripts and data (`/data`) by doing:
```bash
chmod -R o=u /data/
```

The Singularity image is build automatically by [Singularity hub](https://singularity-hub.org/collections/3290) and can be download  with:
```
singularity pull shub://iarcbioinfo/acnviewer-singularity
```

Then aCNViewer can be run, for example to generate histograms from ASCAT-like input file (https://github.com/FJD-CEPH/aCNViewer#othercnvformats):
```
singularity exec acnviewer_latest.sif python /data/aCNViewer/code/aCNViewer.py -f input_cnv.txt -t acnviewer_output --refBuild hg38 -b /data/aCNViewer_DATA/bin/
```

Note that other modes of aCNViewer have not been tested.

Reference: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0189334
