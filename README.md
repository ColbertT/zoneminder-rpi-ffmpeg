# zoneminder-rpi-ffmpeg

## Overview

The perfermence of zoneminder image for raspberry pi4 cannot use hardware acceleration by default, so it has heavy CPU load when the input stream is codec by h264. I spent a few days and find out a way to fix it. It is to rebuild the ffmpeg program and relative libs.

## Key Information

The root cause is the zmc process cannot find out the correct decoder at line 457 in zm_ffmpeg_camera.cpp file - avcodec_find_decoder_by_name("h264_mmal") return false.

## Building

```bash
docker build -t zoneminder-rpi-ffmpeg -f Dockerfile.armv7-rpi .
```

## Running

```bash
docker run -d --shm-size=4096m -e TZ=America/Nome --net=host --device=/dev/vchiq --name zoneminder-rpi zoneminder-rpi-ffmpeg
```

## About

* https://github.com/angeloavv/rpi-zoneminder
* https://github.com/mmastrac/ffmpeg-omx-rpi-docker
