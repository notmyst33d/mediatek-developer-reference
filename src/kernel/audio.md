<div class="warning">
Mediatek ALSA drivers are highly unstable when using ALSA API manually and they may cause a kernel panic. Consider interfacing with Audio HAL instead. 
</div>

# Audio
Modern Mediatek ALSA drivers use kernel streaming, multiple buffers are allocated and are routed dynamically using [ALSA controls](#alsa-controls).

## Terminology
- **ADDA** - Analog to Digital & Digital to Analog Converter. Usually used for headphones due to ADDA's ability to handle both headset and it's microphone.
- **I2S** - Inter-Integrated Circuit Sound. Usually used for speakers.
- **DL** - Downlink/sink.
- **UL** - Uplink/source.

## Buffers
- `Playback_1`/`DL1` - Default playback buffer.
- `Playback_2`/`DL2` - Isolated deep buffer.
- `Playback_3`/`DL3` - Isolated deep buffer fallback, used when `Playback_2` isn't available.
- `Playback_12`/`DL12` - VoIP playback buffer.

## ALSA Controls
### Scenario
- `deep_buffer_scenario` - Controls if route is using deep buffer or not.

### Headphones
- `HPL Mux` - Headphones left channel muxer. Default is `Open`, should switch to `Audio Playback` when playing audio through headphones.
- `HPR Mux` - Headphones right channel muxer. Default is `Open`, should switch to `Audio Playback` when playing audio through headphones.
- `ADDA_DL_GAIN` - ADDA total gain.

### Routing
*Note: Usually `CH1` is left channel and `CH2` is right channel. It's not possible to route `CH1` to `CH2` and vice versa.*
- `ADDA_DL_CHn DLx_CHn` - Route channel `n` of ADDA to channel `n` of downlink `x`.
- `I2Sx_CHn DLy_CHn` - Route channel `n` of I2S device `x` to channel `n` of downlink `y`.

## HiFi Audio
You can use `S24_LE` and `S32_LE` sample formats to get HiFi audio.

If you get distorted audio when using `S24_LE` or `S32_LE` sample formats, it means your volume is too high, you can try lowering it by 48dB:
```shell
# ffmpeg -i [path to audio file] -af volume=-48dB -ac 2 -ar 48000 -f s32le - | aplay -D hw:0,2 -r 48000 -c 2 -f S32_LE
```

*Note: Some devices might have problems with sample rates above 48000.*

## Examples
### Routing deep buffer to headphones and playing audio using aplay
```shell
# amixer sset "HPL Mux" "Audio Playback"
# amixer sset "HPR Mux" "Audio Playback"
# amixer sset "ADDA_DL_CH1 DL2_CH1" on
# amixer sset "ADDA_DL_CH2 DL2_CH2" on
# amixer sset "deep_buffer_scenario" on
# aplay -D hw:0,2 [path to .wav file]
```
