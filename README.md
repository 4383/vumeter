# Vumeter

```bash
podman run --rm -v $(pwd):/tmp:Z -w /tmp \
  jrottenberg/ffmpeg:6.0-ubuntu \
  -i harvard.wav \
  -filter_complex "[0:a]showfreqs=s=1280x720:mode=bar:fscale=log:colors=white[raw]; \
                   [raw]colorchannelmixer=rr=0.0:rg=0.0:rb=0.0: \
                                        gr=0.0:gg=0.98:gb=0.0: \
                                        br=0.0:bg=0.0:bb=1.0[vis]; \
                   color=color=green@1.0:s=1280x720:d=18.36[bg]; \
                   [bg][vis]overlay=format=auto" \
  -c:v libx264 -pix_fmt yuv420p -shortest vumetre.mp4
```
