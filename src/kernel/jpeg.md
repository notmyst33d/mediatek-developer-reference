# JPEG
VPU has a JPEG codec, but it's not exposed via V4L2 M2M API, instead it's provided via `/proc/mtk_jpeg`.

Buffers provided to the API should be allocated using [M4U](m4u.md).
