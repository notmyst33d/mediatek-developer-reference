<div class="warning">
Kernel drivers expect vpud to run in userspace. Encoding and decoding won't work without vpud.
</div>

# VCU and VPU
**VCU (Video Communication Unit)** and **VPU (Video Processor Unit)** are used for encoding and decoding videos. Both terms can be used interchangeably, but VPU is a more prevalent term, it will be used throughout this book.

## API
Mediatek provides [V4L2 M2M](https://www.kernel.org/doc/html/v6.1/userspace-api/media/v4l/dev-encoder.html) API for high-level VPU operations.

`/dev/vcu` and `/dev/vpu` devices are meant for vpud and don't have any relevant encoding/decoding interfaces.

## DMA
Most kernel configurations enable `CONFIG_VB2_MEDIATEK_DMA_CONTIG`. When this config is enabled, kernel drivers use their own `mtk_dma_contig_memops`, this struct lacks `VB2_MMAP` and `VB2_USERPTR` support, which breaks many applications that use these modes.

## Devices
- `/dev/video0` - Decoding.
- `/dev/video1` - Encoding.

## Decoding Support
| SoC    | AVC | HEVC | VP8 | VP9 | AV1 |
| ------ | --- | ---- | --- | --- | --- |
| MT6768 | ✅  | ✅   | ✅  | ✅  | ❌  |

## Encoding Support
| SoC    | AVC | HEVC | VP8 | VP9 | AV1 |
| ------ | --- | ---- | --- | --- | --- |
| MT6768 | ✅  | ✅   | ❌  | ❌  | ❌  |
