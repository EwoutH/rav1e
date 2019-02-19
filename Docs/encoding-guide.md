# Rav1e Encoding Guide

# Input
rav1e expects a `.y4m` 

# Options
All rav1e options can be viewed using the `rav1e --help` command, and are included in *Appendix II: Parameters* below.

# Speed settings
Speed parameters are defined in [api.rs](https://github.com/xiph/rav1e/blob/master/src/api.rs). The CLI exposes only a preset using `-s` or `--speed`. Default is `3`, possible values are `0` to `10`.

The table below states which features are enabled at which preset.

|                      |    -s 0    |    -s 1    |       -s 2       |       -s 3       |  -s 4  |  -s 5  |  -s 6  |  -s 7  |  -s 8  |  -s 9  |  -s 10 |
|----------------------|:----------:|:----------:|:----------------:|:----------------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|
| min_block_size       |     4X4    |     4X4    |        8X8       |       16X16      |  32X32 |  64X64 |  64X64 |  64X64 |  64X64 |  64X64 |  64X64 |
| multiref             |    TRUE    |    TRUE    |       TRUE       |       FALSE      |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |
| fast_deblock         |    FALSE   |    FALSE   |       FALSE      |       FALSE      |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |
| reduced_tx_set       |    FALSE   |    FALSE   |       TRUE       |       TRUE       |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |
| tx_domain_distortion |    FALSE   |    FALSE   |       FALSE      |       FALSE      |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |  TRUE  |
| encode_bottomup      |    TRUE    |    FALSE   |       FALSE      |       FALSE      |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |
| rdo_tx_decision      |    TRUE    |    TRUE    |       TRUE       |       TRUE       |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |
| prediction_modes     | ComplexAll | ComplexAll | ComplexKeyframes | ComplexKeyframes | Simple | Simple | Simple | Simple | Simple | Simple | Simple |
| include_near_mvs     |    TRUE    |    TRUE    |       TRUE       |       FALSE      |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |
| no_scene_detection   |    FALSE   |    FALSE   |       FALSE      |       FALSE      |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  FALSE |  TRUE  |

# Appendix II: Parameters
```
rav1e --help
rav1e 0.1.0
AV1 video encoder

USAGE:
    rav1e [FLAGS] [OPTIONS] <INPUT> --output <OUTPUT>

FLAGS:
    -v, --verbose    Verbose logging; outputs info for every frame
        --psnr       Calculate and display PSNR metrics
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
        --threads <THREADS>                        Set the threadpool size [default: 0]
    -o, --output <OUTPUT>                          Compressed AV1 in IVF video output
        --stats <STATS_FILE>                       Custom location for first-pass stats file [default: rav1e_stats.json]
    -p, --pass <PASS>
            Specify first-pass or second-pass to run as a two-pass encode; If not provided, will run a one-pass encode
            [possible values: 1, 2]
    -l, --limit <LIMIT>                            Maximum number of frames to encode [default: 0]
        --quantizer <QP>                           Quantizer (0-255), smaller values are higher quality [default: 100]
    -b, --bitrate <BITRATE>                        Bitrate (kbps)
    -s, --speed <SPEED>                            Speed level (0 is best quality, 10 is fastest) [default: 3]
    -i, --min-keyint <MIN_KEYFRAME_INTERVAL>       Minimum interval between keyframes [default: 12]
    -I, --keyint <KEYFRAME_INTERVAL>               Maximum interval between keyframes [default: 240]
        --low_latency <LOW_LATENCY>                Low latency mode; disables frame reordering [default: false]
        --tune <TUNE>
            Quality tuning [default: Psychovisual]  [possible values: Psnr, Psychovisual]

        --range <PIXEL_RANGE>
            Pixel range [default: unspecified]  [possible values: Unspecified, Limited, Full]

        --primaries <COLOR_PRIMARIES>
            Color primaries used to describe color parameters [default: unspecified]  [possible values: BT709,
            Unspecified, BT470M, BT470BG, ST170M, ST240M, Film, BT2020, ST428, P3DCI, P3Display, Tech3213]
        --transfer <TRANSFER_CHARACTERISTICS>
            Transfer characteristics used to describe color parameters [default: unspecified]  [possible values: BT1886,
            Unspecified, BT470M, BT470BG, ST170M, ST240M, Linear, Logarithmic100, Logarithmic316, XVYCC, BT1361E, SRGB,
            BT2020Ten, BT2020Twelve, PerceptualQuantizer, ST428, HybridLogGamma]
        --matrix <MATRIX_COEFFICIENTS>
            Matrix coefficients used to describe color parameters [default: unspecified]  [possible values: Identity,
            BT709, Unspecified, BT470M, BT470BG, ST170M, ST240M, YCgCo, BT2020NonConstantLuminance,
            BT2020ConstantLuminance, ST2085, ChromaticityDerivedNonConstantLuminance,
            ChromaticityDerivedConstantLuminance, ICtCp]
        --mastering_display <MASTERING_DISPLAY>
            Mastering display primaries in the form of G(x,y)B(x,y)R(x,y)WP(x,y)L(max,min) [default: unspecified]

        --content_light <CONTENT_LIGHT>
            Content light level used to describe content luminosity (cll,fall) [default: 0,0]

    -r <RECONSTRUCTION>                            Outputs a Y4M file containing the output from the decoder

ARGS:
    <INPUT>    Uncompressed YUV4MPEG2 video input
```
