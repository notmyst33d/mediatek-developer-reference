# Audio
Mediatek platform uses ALSA, it exposes a lot of controls which are used to perform various tasks (e.g. switching routes).

## Terminology
- **ADDA** - Analog to Digital & Digital to Analog Converter. Usually used for headphones due to ADDA's ability to handle headset microphones.
- **I2S** - Inter-Integrated Circuit Sound. Usually used for speakers.
- **DL** - Downlink/sink.
- **UL** - Uplink/source.

## Buffers
- `Playback_1`/`DL1` - Default multimedia buffer.
- `Playback_2`/`DL2` - Deep buffer for HiFi.
- `Playback_3`/`DL3` - Unknown, might be also available for multimedia.
- `Playback_12`/`DL12` - Unknown, might be also available for multimedia.

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

