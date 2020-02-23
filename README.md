# ionoreporter
Ionoreporter is a small app that produce pdf files of a set of images,
specifically ionograms. Since version 2 it reads the data from Juliusruh's
ionogram using `tesseract` OCR (via gosseract) and has the ability to push that
information to a Slack app using a webhook (hooks.slack.com).

The app is written in [Go](https://golang.org) and
builds with GNU Make (using a Makefile). The Makefile can also be used to build
a docker image to run ionoreporter as a container.

## Dependencies

Golang 1.10 (probably works with earlier too), Docker and GNU Make.

## Simple installation

If you have `go` already installed, you can run `go get
github.com/sa6mwa/ionoreporter` and you will have the `ionoreporter` binary in
your `$GOPATH/bin`.

## Building and running

```bash
# See Makefile for more info.
# Default build env is amd64 and whatever uname -s says.
make all
make run
# If you have docker, you can build and run ionoreporter as a container:
make docker
make docker-run
```

## Example

```
$ make docker-run
docker run -u 1000:1000 -ti --rm -v /home/sa6mwa/ionoreporter/output:/destination -e IRPT_OUTDIR=/destination ionoreporter:1.0
INFO[2019-11-04T21:09:25Z] Starting ionoreporter 1.0, IRPT_OUTDIR == /destination 
INFO[2019-11-04T21:09:25Z] Downloading https://www.iap-kborn.de/fileadmin/user_upload/MAIN-abteilung/radar/Radars/Ionosonde/Plots/LATEST.PNG 
INFO[2019-11-04T21:09:26Z] Downloading http://www.tgo.uit.no/ionosonde/latest.gif 
INFO[2019-11-04T21:09:26Z] Downloading http://www2.irf.se/ionogram/dynasonde_kir/sao/latest.gif 
INFO[2019-11-04T21:09:26Z] Downloading http://www2.irf.se/ionogram/plots/ionoLy.gif 
INFO[2019-11-04T21:09:27Z] kiruna ionogram saved as /tmp/ionoreporter-235787570.gif 
INFO[2019-11-04T21:09:27Z] lycksele ionogram saved as /tmp/ionoreporter-415884521.gif 
INFO[2019-11-04T21:09:27Z] juliusruh ionogram saved as /tmp/ionoreporter-626629632.png 
INFO[2019-11-04T21:09:27Z] tromso ionogram saved as /tmp/ionoreporter-512875359.gif 
INFO[2019-11-04T21:09:27Z] Saving /destination/ionoreport-20191104T210927.pdf 
INFO[2019-11-04T21:09:27Z] Waiting 15m0s until next run                 
```
