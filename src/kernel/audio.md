# Audio
Mediatek platform uses ALSA, except it exposes a lot of controls which are used to perform various tasks (e.g. switching routes).

## Buffers
- `Playback_1` - default multimedia buffer
- `Playback_2` - deep buffer for HiFi

## Switching route to headphones and playing audio using aplay
```shell
# aplay -D hw:0,0 [path to .wav file]
```
