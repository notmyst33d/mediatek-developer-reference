# VCU/VPU
Mediatek provides [V4L2 M2M](https://www.kernel.org/doc/html/v6.1/userspace-api/media/v4l/dev-encoder.html) API for high-level VCU/VPU operations.

It's possible to use VCU/VPU directly using `/dev/vcu` or `/dev/vpu` but the API is very limited.

## Devices
- `/dev/video0` - Decoding.
- `/dev/video1` - Encoding.

## Encoding Support
| SoC    | AVC | HEVC | VP8 | VP9 | AV1 |
| ------ | --- | ---- | --- | --- | --- |
| MT6768 | ✅  | ✅   | ❌  | ❌  | ❌  |

## Decoding Support
| SoC    | AVC | HEVC | VP8 | VP9 | AV1 |
| ------ | --- | ---- | --- | --- | --- |
| MT6768 | ✅  | ✅   | ✅  | ✅  | ❌  |